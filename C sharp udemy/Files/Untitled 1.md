```
using Spectre.Console;
using TicTacToe.DTO;
using TicTacToe.Enums;
using TicTacToe.Models;
using TicTacToe.Services;
using TicTacToe.Views;

namespace TicTacToe.Controllers
{
    public class GameController
    {
        public GameService GameService { get; set; }
        public UserDTO UserDTO { get; set; }

        public GameController(GameService gameService, UserDTO userDTO)
        {
            GameService = gameService;
            UserDTO = userDTO;
        }

        public async Task Run()
        {
            while(true)
            {
                ConsoleView.PrintHeader("Game Type");
                GameType gameType = AnsiConsole.Prompt(
               new SelectionPrompt<GameType>()
               .Title("Choose an option:")
               .PageSize(10)
               .AddChoices(Enum.GetValues<GameType>()));

                Func<Board, (int row, int col)>? GetBotMove = null;
                switch (gameType)
                {
                    case GameType.SinglePlayer:
                        GetBotMove = ChoseGameMode(out GameMode gameMode);
                        await PlayGame(true, GetBotMove, UserDTO, "Bot",  gameMode, gameType);
                        break;

                    case GameType.MultiPlayer:
                        string opponentName = ConsoleView.GetInput<string>("Enter the Opponent's name: ", "Opponent name cannot be Empty. Enter a valid name.");
                        await PlayGame(false, GetBotMove, UserDTO, opponentName, null, gameType);
                        break;

                    case GameType.ReturnToMainMenu:
                        return;
                }
            }
            
        }

        private async Task PlayGame(bool IsSinglePlayerMode, Func<Board, (int row, int col)>? GetBotMove, UserDTO? userDTO, string opponentName, GameMode? gameMode, GameType gameType)
        {
            Board board = new Board(3);
            BoardView boardView = new BoardView();
            GameState gameState = new GameState();

            string statusMessage = string.Empty;
            ResponseStatus statusCode = ResponseStatus.Info;

            while (!gameState.IsWinner && !gameState.IsDraw)
            {
                Console.Clear();
                boardView.DrawBoard(board, true, gameState.Row, gameState.Col);

                GameService.CheckGameStatus(board, gameState, out CellState? winner);
                if (gameState.IsWinner)
                {
                    string winnerName = winner == CellState.X ? userDTO.UserName : opponentName;
                    Guid? winnerGuid = winner == CellState.X ? userDTO.Id : null;
                    TimeSpan gameDuration = DateTime.Now - gameState.StartTime;
                    GameData gameData = new GameData(userDTO.Id, null, gameState.Moves, winnerGuid, gameDuration, gameMode, gameType, GameOutcome.Win, DateTime.Now, userDTO.UserName, opponentName, winnerName);
                    GameService.SaveGame(gameData);
                    ConsoleView.PrintResponse($"Player - {winnerName} has won!!!", ResponseStatus.Success);
                    break;
                }
                else if (gameState.IsDraw)
                {
                    TimeSpan gameDuration = DateTime.Now - gameState.StartTime;
                    GameData gameData = new GameData(userDTO.Id, null, gameState.Moves, null, gameDuration, gameMode, gameType, GameOutcome.Draw, DateTime.Now, userDTO.UserName, opponentName, null);
                    GameService.SaveGame(gameData);
                    ConsoleView.PrintResponse("The match ended in a draw.", ResponseStatus.Info);
                    break;
                }

                ConsoleView.PrintResponse(statusMessage, statusCode);
                statusMessage = string.Empty;
                if (gameState.IsAborted)
                {
                    TimeSpan gameDuration = DateTime.Now - gameState.StartTime;
                    GameData gameData = new GameData(userDTO.Id, null, gameState.Moves, null, gameDuration, gameMode, gameType, GameOutcome.Aborted, DateTime.Now, userDTO.UserName, opponentName, null);
                    GameService.SaveGame(gameData);
                    break;
                }

                boardView.WriteGameMetaData(gameState.CurrentSymbol == CellState.X ? userDTO.UserName : opponentName, gameState.CurrentSymbol);
                boardView.WriteInstruction();

                if (gameState.CurrentSymbol == CellState.O && IsSinglePlayerMode)
                {
                    await Task.Delay(1000);
                    if(GetBotMove != null)
                    {
                        (int bestRow, int bestCol) = GetBotMove(board);
                        board.SetCell(bestRow, bestCol, CellState.O);
                        gameState.Moves.Add(new Move(board.GetIndex(bestRow, bestCol), CellState.O));
                    }

                    gameState.CurrentSymbol = CellState.X;
                    continue;
                }

                ConsoleKeyInfo keyInfo = Console.ReadKey(true);
                switch (keyInfo.Key)
                {
                    case ConsoleKey.Escape:
                        gameState.IsAborted = true;
                        statusMessage = "Game Aborted";
                        statusCode = ResponseStatus.Failure;
                        continue;

                    case ConsoleKey.R:
                        GameService.ResetGame(board, gameState);
                        continue;

                    case ConsoleKey.Enter:
                    case ConsoleKey.Spacebar:
                        Response? response = GameService.TryMakeMove(board, gameState);
                        if (response != null)
                        {
                            statusCode = ResponseStatus.Failure;
                            statusMessage = response.Message;
                            continue;
                        }

                        break;

                    case ConsoleKey.UpArrow:
                    case ConsoleKey.DownArrow:
                    case ConsoleKey.LeftArrow:
                    case ConsoleKey.RightArrow:
                        Response? responseData = GameService.TryMoveCursor(board, gameState, keyInfo.Key);
                        if (responseData != null)
                        {
                            statusCode = ResponseStatus.Failure;
                            statusMessage = responseData.Message;
                            continue;
                        }

                        break;
                }
            }

            ConsoleView.PrintResponse("Press any key to return to the menu", ResponseStatus.Warning);
            Console.ReadKey(true);
        }

        public Func<Board, (int row, int col)>? ChoseGameMode(out GameMode gameMode)
        {
            Console.Clear();
            ConsoleView.PrintHeader("Game Mode");
            GameMode choice = AnsiConsole.Prompt(
           new SelectionPrompt<GameMode>()
           .Title("Choose an option:")
           .PageSize(10)
           .AddChoices(Enum.GetValues<GameMode>()));
            BotService botService = new BotService();
            gameMode = choice;
            Func<Board, (int row, int col)>? GetBotMove = null;
            switch (choice)
            {
                case GameMode.Easy:
                    GetBotMove = botService.GetEasyMove;
                    break;

                case GameMode.Medium:
                    GetBotMove = botService.GetMediumMove;
                    break;

                case GameMode.Hard:
                    GetBotMove = botService.GetHardMove;
                    break;
            }

            return GetBotMove;
        }
    }
}
```

```
using System.Text.RegularExpressions;
using TicTacToe.DTO;
using TicTacToe.Enums;
using TicTacToe.Models;
using TicTacToe.Services;
using TicTacToe.Views;

namespace TicTacToe.Controllers
{
    public class GameHistoryController
    {
        GameService GameService;
        ReplayService ReplayService;

        public GameHistoryController(GameService GameService)
        {
            this.GameService = GameService;
        }

        public void ViewGameHistory(Guid userId)
        {
            List<GameData> gameHistorys = GameService.GetGameHistory(userId);
            int count = 0;
            ConsoleView.PrintTable<GameData>(
                gameHistorys,
                 new string[]
                {
                    "S.No",
                    "Played At",
                    "Type",
                    "Mode",
                    "Player X",
                    "Player Y",
                    "Winner",
                    "Outcome",
                    "Duration(min:sec)"
                },
                 new Func<GameData, object>[]
                {
                    gameData => ++count,
                    gameData => gameData.PlayedAt.ToString("dd-MM-yyyy HH:mm"),
                    gameData => gameData.GameType,
                    gameData => gameData.GameMode == null ? "Manual" : gameData.GameMode,
                    gameData => gameData.PlayerXName,
                    gameData => gameData.PlayerYName,
                    gameData => gameData.WinnerName ?? "-",
                    gameData => gameData.GameOutcome,
                    gameData => gameData.Duration.ToString(@"mm\:ss"),
                }
                );

            string userInput = ConsoleView.GetInput<string>(
                "Do you want to Action Replay a Game[Y/N]",
                "Invalid input. Enter [Y/N]",
                (input) => input.Equals("Y", StringComparison.OrdinalIgnoreCase) || input.Equals("N", StringComparison.OrdinalIgnoreCase),
                "Invalid Input. Enter [Y/N]");

            bool needReplay = userInput.Equals("Y", StringComparison.OrdinalIgnoreCase);
            if (needReplay)
            {
                int sNo = ConsoleView.GetInput<int>("enter S.No of the game to replay", "Enter a valid whole number");
                GameData gameData = gameHistorys[sNo - 1];
                ReplayGame(gameData);
            }
        }


        public void ReplayGame(GameData gameData)
        {
            Board board = new Board(3);
            BoardView boardView = new BoardView();
            ReplayService replayService = new ReplayService(gameData.Moves, board);
            string statusMessage = string.Empty;
            ResponseStatus statusType = ResponseStatus.Info;

            while (true)
            {
                Console.Clear();
                boardView.DrawBoard(board, false);

                if(!replayService.HasNextMove())
                {
                    switch (gameData.GameOutcome)
                    {
                        case GameOutcome.Win:
                            ConsoleView.PrintResponse($"Winner: {gameData.WinnerName}", ResponseStatus.Success);
                            break;

                        case GameOutcome.Draw:
                            ConsoleView.PrintResponse("Game ended in Draw", ResponseStatus.Info);
                            break;

                        case GameOutcome.Aborted:
                            ConsoleView.PrintResponse("Game was Aborted", ResponseStatus.Warning);
                            break;
                    }
                }


                ConsoleView.PrintResponse(statusMessage, statusType);
                statusMessage = string.Empty;
                CellState? currSymbol = replayService.GetCurrentMoveSymbol();
                if (currSymbol != null)
                {
                    string playerName = currSymbol == CellState.X ? gameData.PlayerXName : gameData.PlayerYName;
                    boardView.WriteGameMetaDataForReplayGame(playerName, currSymbol.Value);
                }
                boardView.WriteInstructionForReplayGame();

                ConsoleKeyInfo keyInfo = Console.ReadKey(true);
                switch (keyInfo.Key)
                {
                    case ConsoleKey.Escape:
                        return;

                    case ConsoleKey.LeftArrow:
                        if (!replayService.HasPreviousMove())
                        {
                            statusMessage = "No previous moves";
                            statusType = ResponseStatus.Warning;
                            continue;
                        }
                        replayService.UndoPreviousMove();
                        break;

                    case ConsoleKey.RightArrow:
                        if (!replayService.HasNextMove())
                        {
                            statusMessage = "No more moves";
                            statusType = ResponseStatus.Warning;
                            continue;
                        }
                        replayService.MoveNext();
                        break;
                }
            }
        }
    }
}
```


```
using Spectre.Console;
using TicTacToe.DTO;
using TicTacToe.Enums;
using TicTacToe.Models;
using TicTacToe.Services;
using TicTacToe.Views;

namespace TicTacToe.Controllers
{
    public class MainController
    {
        public async Task RouteToOption(UserDTO? userDTO)
        {
            while(true)
            {
                ConsoleView.PrintHeader("Menu");
                MainMenu choice = AnsiConsole.Prompt(
               new SelectionPrompt<MainMenu>()
               .Title("Choose an option:")
               .PageSize(10)
               .AddChoices(Enum.GetValues<MainMenu>()));

                switch (choice)
                {
                    case MainMenu.PlayGame:
                        GameController gameController = new GameController(new GameService(), userDTO);
                        await gameController.Run();
                        break;

                    case MainMenu.ViewGameHistory:
                        GameHistoryController gameHistoryController = new GameHistoryController(new GameService());
                        ConsoleView.PrintHeader("Game History");
                        gameHistoryController.ViewGameHistory(userDTO.Id);
                        
                        ConsoleView.PrintResponse("Press any key to return to Main menu", ResponseStatus.Warning);
                        Console.ReadKey();
                        break;

                    case MainMenu.AboutGame:
                        ConsoleView.PrintHeader("About Game");
                        ConsoleView.ShowGameRules();
                        ConsoleView.PrintResponse("Press any key to return to Main menu", ResponseStatus.Warning);
                        Console.ReadKey();
                        break;

                    case MainMenu.Exit:
                        Console.Clear();
                        Environment.Exit(0);
                        break;
                }
            }
        }
    }
}
```

```
using TicTacToe.Enums;
using TicTacToe.Models;

namespace TicTacToe.Services
{
    public class GameService
    {
        private const string GameHistoryFileDirectory = "./ReplayHistory";
        public void ResetGame(Board board, GameState state)
        {
            board.ClearBoard();
            state.Row = 0;
            state.Col = 0;
            state.CurrentSymbol = CellState.X;
            state.IsWinner = false;
            state.IsDraw = false;
            state.IsAborted = false;
        }

        public Response? TryMakeMove(Board board, GameState gameState)
        {
            if (board.GetCell(gameState.Row, gameState.Col) != CellState.Empty)
            {

                return new Response("Cell already occupied", ResponseStatus.Failure);
            }

            board.SetCell(gameState.Row, gameState.Col, gameState.CurrentSymbol);
            gameState.Moves.Add(new Move(board.GetIndex(gameState.Row, gameState.Col), gameState.CurrentSymbol));
            gameState.CurrentSymbol = gameState.CurrentSymbol == CellState.X ? CellState.O : CellState.X;
            return null;
        }

        public void CheckGameStatus(Board board, GameState gameState, out CellState? winner)
        {
            gameState.IsWinner = board.IsWinner(out winner);
            if(!gameState.IsWinner)
            {
                gameState.IsDraw = board.IsDrawAfterWinnerCheck();
            }
        }

        public void SaveGame(GameData gameData)
        {
            List<GameData> gameDatas = JsonFileHandler.LoadFromFile<GameData>(Path.Combine(GameHistoryFileDirectory, $"{gameData.PlayerXId}.json"));
            gameDatas.Add(gameData);
            JsonFileHandler.SaveToFile<GameData>(Path.Combine(GameHistoryFileDirectory, $"{gameData.PlayerXId}.json"), gameDatas);
        }

        public Response? TryMoveCursor(Board board, GameState gameState, ConsoleKey key)
        {
            switch (key)
            {
                case ConsoleKey.RightArrow:
                    if (gameState.Col + 1 >= board.Dimension)
                    {
                        return new Response("Index out of range", ResponseStatus.Failure);
                    }

                    gameState.Col++;
                    return null;

                case ConsoleKey.LeftArrow:
                    if (gameState.Col - 1 < 0)
                    {
                        return new Response("Index out of range", ResponseStatus.Failure);
                    }

                    gameState.Col--;
                    break;

                case ConsoleKey.UpArrow:
                    if (gameState.Row - 1 < 0)
                    {
                        return new Response("Index out of range", ResponseStatus.Failure);
                    }

                    gameState.Row--;
                    break;

                case ConsoleKey.DownArrow:
                    if (gameState.Row + 1 >= board.Dimension)
                    {
                        return new Response("Index out of range", ResponseStatus.Failure);
                    }

                    gameState.Row++;
                    break;
            }

            return null;
        }

        public List<GameData> GetGameHistory(Guid userId)
        {
            return JsonFileHandler.LoadFromFile<GameData>(Path.Combine(GameHistoryFileDirectory, $"{userId}.json"));
        }
    }
}
```


```
using TicTacToe.Enums;
using TicTacToe.Models;

namespace TicTacToe.Services
{
    class ReplayService
    {
        private List<Move> _moves;
        private int _currentIndex;
        private Board _board;

        public ReplayService(List<Move> moves, Board board)
        {
            _moves = moves;
            _currentIndex = -1;
            _board = board;
        }

        public bool HasNextMove()
        {
            return _currentIndex < _moves.Count - 1;
        }

        public bool HasPreviousMove()
        {
            return _currentIndex >= 0;
        }

        public CellState? GetCurrentMoveSymbol()
        {
            if (_currentIndex < 0 || _currentIndex >= _moves.Count)
            {
                return null;
            }

            return _moves[_currentIndex].CellState;
        }

        public bool MoveNext()
        {
            if (!HasNextMove())
            {
                return false;
            }

            _currentIndex++;
            Move move = _moves[_currentIndex];
            _board.SetCell(move.Position, move.CellState);
            return true;
        }

        public bool UndoPreviousMove()
        {
            if(!HasPreviousMove())
            {
                return false;
            }

            var move = _moves[_currentIndex];
            _board.SetCell(move.Position, CellState.Empty);
            _currentIndex--;
            return true;
        }
    }
}
```