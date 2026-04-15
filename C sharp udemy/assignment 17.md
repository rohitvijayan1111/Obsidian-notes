
# PluginInterface
```
namespace PluginInterface
{
    /// <summary>
    /// Defines a contract for text processing plugins.
    /// Implementations should take an input string and return a processed result.
    /// </summary>
    public interface ITextPlugin
    {
        /// <summary>
        /// Processes the given input text and returns the transformed output.
        /// </summary>
        /// <param name="input">The input text to process.</param>
        /// <returns>The processed output string.</returns>
        string Process(string input);
    }
}
```


# ReverseTextPlugin
```
namespace ReverseTextPlugin
{
    using PluginInterface;

    /// <summary>
    /// A plugin that reverses the input text.
    /// </summary>
    public class ReversePlugin : ITextPlugin
    {
        /// <summary>
        /// Reverses the characters in the given input string.
        /// </summary>
        /// <param name="input">The input text to reverse.</param>
        /// <returns>The reversed string.</returns>
        public string Process(string input)
        {
            char[] charArray = input.ToCharArray();
            Array.Reverse(charArray);
            return new string(charArray);
        }
    }
}
```


```
namespace UpperCasePlugin
{
    using PluginInterface;

    /// <summary>
    /// A plugin that converts input text to uppercase.
    /// </summary>
    public class UppercasePlugin : ITextPlugin
    {
        /// <summary>
        /// Converts the given input string to uppercase.
        /// </summary>
        /// <param name="input">The input text to convert.</param>
        /// <returns>The uppercase version of the input string.</returns>
        public string Process(string input)
        {
            return input.ToUpper();
        }
    }

}
```


```
namespace WordCountPlugin
{
    using PluginInterface;

    /// <summary>
    /// A plugin that processes input text and returns the total word count.
    /// </summary>
    public class WordCountPlugin : ITextPlugin
    {
        /// <summary>
        /// Counts the number of words in the given input string.
        /// </summary>
        /// <param name="input">The input text to analyze.</param>
        /// <returns>A formatted string containing the word count.</returns>
        public string Process(string input)
        {
            int wordCount = input.Split(new[] { ' ', '\n' }).Length;
            return $"Word count: {wordCount}";
        }
    }
}
```


```
namespace Assignments
{
    /// <summary>
    /// Contains application wide constant values used for plugin and file paths.
    /// </summary>
    public static class AppConstants
    {
        /// <summary>
        /// Relative file path to the PlayerStats plugin DLL.
        /// </summary>
        public const string PlayerStatsDllFileLocation = "../../../PlayerStatsPlugin.dll";

        /// <summary>
        /// Gets the full path to the Plugins folder based on the application's base directory.
        /// </summary>
        public static readonly string PluginFolderPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "../../../Plugins");
    }
}
```


```
using System.Reflection;
using ConsoleViewPackage;

namespace Assignments
{
    /// <summary>
    /// Provides functionality to inspect and display metadata of an assembly,
    /// including its types, methods, fields, properties, and events.
    /// </summary>
    public class AssemblyInspector
    {
        /// <summary>
        /// Executes the assembly inspection process by loading the assembly
        /// and printing metadata details for each type.
        /// </summary>
        public void Execute()
        {
            Assembly assembly = Assembly.LoadFrom(AppConstants.PlayerStatsDllFileLocation);

            ConsoleView.PrintHeader("Assembly Info");

            Type[] types = DisplayTypesAndReturnTypes(assembly);

            foreach (Type type in types)
            {
                ConsoleView.PrintHeader($"Class: {type.Name}");
                PrintMethodDetails(type);
                PrintFieldDetails(type);
                PrintEventDetails(type);
                PrintPropertyDetails(type);
            }
        }

        private static void PrintPropertyDetails(Type type)
        {
            PropertyInfo[] propertyList = type.GetProperties(
                                BindingFlags.Public |
                                BindingFlags.NonPublic |
                                BindingFlags.Instance |
                                BindingFlags.Static |
                                BindingFlags.DeclaredOnly);

            if (propertyList.Length == 0)
            {
                ConsoleView.PrintResponse("No properties available", ResponseStatus.Failure);
            }
            else
            {
                foreach (PropertyInfo property in propertyList)
                {
                    ConsoleView.PrintSubHeader($"Property: {property.Name}");
                    ConsoleView.PrintResponse($"Type: {property.PropertyType.Name}", ResponseStatus.Warning);
                }
            }
        }

        private static void PrintEventDetails(Type type)
        {
            EventInfo[] eventList = type.GetEvents(
                                BindingFlags.Public |
                                BindingFlags.NonPublic |
                                BindingFlags.Instance |
                                BindingFlags.Static |
                                BindingFlags.DeclaredOnly);

            if (eventList.Length == 0)
            {
                ConsoleView.PrintResponse("No events available", ResponseStatus.Failure);
            }
            else
            {
                foreach (EventInfo eventInfo in eventList)
                {
                    ConsoleView.PrintSubHeader($"Event: {eventInfo.Name}");
                    ConsoleView.PrintResponse($"Event Handler Type: {eventInfo.EventHandlerType?.Name ?? "-"}, Is Multicast: {eventInfo.IsMulticast}", ResponseStatus.Warning);

                    MethodInfo? addMethod = eventInfo.GetAddMethod(true);
                    MethodInfo? removeMethod = eventInfo.GetRemoveMethod(true);

                    ConsoleView.PrintResponse($"Has Add Method: {addMethod != null}, Has Remove Method: {removeMethod != null}", ResponseStatus.Warning);
                }
            }
        }

        private static void PrintFieldDetails(Type type)
        {
            FieldInfo[] fieldList = type.GetFields(
                                BindingFlags.Public |
                                BindingFlags.NonPublic |
                                BindingFlags.Instance |
                                BindingFlags.Static);

            if (fieldList.Length == 0)
            {
                ConsoleView.PrintResponse("No fields available", ResponseStatus.Failure);
            }
            else
            {
                foreach (FieldInfo field in fieldList)
                {
                    ConsoleView.PrintSubHeader($"Field: {field.Name}");
                    ConsoleView.PrintResponse($"Type: {field.FieldType.Name}", ResponseStatus.Warning);
                    ConsoleView.PrintResponse($"Is Static: {field.IsStatic}, Is Public: {field.IsPublic}, Is InitOnly: {field.IsInitOnly}", ResponseStatus.Warning);
                }
            }
        }

        private static void PrintMethodDetails(Type type)
        {
            MethodInfo[] methodLists = type.GetMethods(
                                BindingFlags.Public |
                                BindingFlags.NonPublic |
                                BindingFlags.Instance |
                                BindingFlags.Static |
                                BindingFlags.DeclaredOnly);

            if (methodLists.Length == 0)
            {
                ConsoleView.PrintResponse("No methods available", ResponseStatus.Failure);
            }

            foreach (MethodInfo methodInfo in methodLists)
            {
                ConsoleView.PrintSubHeader($"Method: {methodInfo.Name}");
                ConsoleView.PrintResponse($"Return Type: {methodInfo.ReturnType.Name}", ResponseStatus.Warning);

                ConsoleView.PrintResponse($"Is Static: {methodInfo.IsStatic}, Is Public: {methodInfo.IsPublic}, Is Virtual: {methodInfo.IsVirtual}", ResponseStatus.Warning);

                ParameterInfo[] parameters = methodInfo.GetParameters();
                if (parameters.Length == 0)
                {
                    ConsoleView.PrintResponse($"Parameters: None", ResponseStatus.Warning);
                    continue;
                }

                string paramList = string.Join(", ", parameters.Select(p => $"{p.ParameterType.Name} {p.Name}"));

                ConsoleView.PrintResponse($"Parameters: {paramList}", ResponseStatus.Warning);
            }
        }

        /// <summary>
        /// Retrieves and displays all types in the assembly along with their metadata.
        /// </summary>
        /// <param name="assembly">The assembly to inspect.</param>
        /// <returns>An array of types defined in the assembly.</returns>
        private static Type[] DisplayTypesAndReturnTypes(Assembly assembly)
        {
            Type[] types = assembly.GetTypes();
            int counter = 0;
            ConsoleView.PrintResponse($"The types available in the Football Stats application\nAssembly details - {assembly.GetName()}: ", ResponseStatus.Success);
            ConsoleView.PrintTable(
            types,
            new string[] { "S.No", "Type Name", "Namespace", "Is Class", "Is Enum", "Is Generic", "Is Public", "Base Type", },
            new Func<Type, object>[] { t => ++counter, t => t.Name, t => t.Namespace ?? "-", t => t.IsClass, t => t.IsEnum, t => t.IsGenericType, t => t.IsPublic, t => t.BaseType?.Name ?? "-" });
            return types;
        }
    }
}
```


```
using System.Reflection;
using ConsoleViewPackage;

namespace Assignments
{
    /// <summary>
    /// Provides functionality to dynamically invoke methods on an object
    /// using Reflection based on a method name provided at runtime.
    /// </summary>
    public class DynamicMethodInvoker
    {
        /// <summary>
        /// Invokes a method on the given object dynamically using the specified method name.
        /// Prompts the user to enter values for method parameters and displays the result.
        /// </summary>
        /// <param name="obj">The object on which the method should be invoked.</param>
        /// <param name="methodName">The name of the method to invoke.</param>
        public void InvokeMethod(object obj, string methodName)
        {
            if (obj == null)
            {
                ConsoleView.PrintResponse("Object cannot be null.", ResponseStatus.Failure);
                return;
            }

            Type type = obj.GetType();
            MethodInfo? method = type.GetMethod(methodName);
            if (method == null)
            {
                ConsoleView.PrintResponse($"{methodName} doesn't exist.", ResponseStatus.Failure);
                return;
            }

            ParameterInfo[] parameters = method.GetParameters();
            object?[] args = new object?[parameters.Length];
            for (int i = 0; i < parameters.Length; i++)
            {
                var param = parameters[i];
                string input = ConsoleView.GetInput<string>($"Enter value for {param.Name} ({param.ParameterType.Name}):", "Invalid input");

                try
                {
                    args[i] = this.ConvertToType(input, param.ParameterType);
                }
                catch
                {
                    ConsoleView.PrintResponse($"Invalid value for parameter '{param.Name}'", ResponseStatus.Failure);
                    return;
                }
            }

            try
            {
                object? result = method.Invoke(obj, args);
                if (method.ReturnType != typeof(void))
                {
                    ConsoleView.PrintResponse($"Result: {result}", ResponseStatus.Success);
                }
                else
                {
                    ConsoleView.PrintResponse("Method executed successfully.", ResponseStatus.Success);
                }
            }
            catch (TargetInvocationException ex)
            {
                ConsoleView.PrintResponse(ex.InnerException?.Message ?? ex.Message, ResponseStatus.Failure);
            }
        }

        private object? ConvertToType(string input, Type targetType)
        {
            if (targetType.IsEnum)
            {
                return Enum.Parse(targetType, input, true);
            }

            return Convert.ChangeType(input, targetType);
        }
    }
}
```


```
using System.Reflection;
using ConsoleViewPackage;

namespace Reflection
{
    /// <summary>
    /// Provides functionality to inspect an object's properties at runtime
    /// and allows the user to modify writable properties interactively.
    /// </summary>
    public class DynamicObjectInspector
    {
        /// <summary>
        /// Inspects the given object by displaying its properties and values,
        /// and allows the user to update property values dynamically.
        /// </summary>
        /// <param name="obj">The object to inspect and modify.</param>
        public void Inspect(object obj)
        {
            if (obj == null)
            {
                ConsoleView.PrintResponse("Object cannot be null.", ResponseStatus.Failure);
                return;
            }

            Type type = obj.GetType();
            while (true)
            {
                ConsoleView.PrintHeader($"Inspecting {type.Name}");
                PropertyInfo[] properties = type.GetProperties();
                for (int i = 0; i < properties.Length; i++)
                {
                    object? value = properties[i].GetValue(obj);
                    Console.WriteLine($"[{i + 1}] {properties[i].Name} = {value}");
                }

                Console.WriteLine("[X] Exit");
                Console.WriteLine();

                string choice = ConsoleView.GetInput<string>("Select property index to edit (or X to exit):", "Invalid input");

                if (choice.Equals("X", StringComparison.OrdinalIgnoreCase))
                {
                    break;
                }

                if (!int.TryParse(choice, out int index) || index < 0 || index > properties.Length)
                {
                    ConsoleView.PrintResponse("Invalid Choice. Enter a valid choice", ResponseStatus.Failure);
                    continue;
                }

                PropertyInfo property = properties[index];
                if (!property.CanWrite)
                {
                    ConsoleView.PrintResponse("Property is read-only.", ResponseStatus.Warning);
                    continue;
                }

                this.UpdateProperty(obj, property);
            }
        }

        private void UpdateProperty(object obj, PropertyInfo property)
        {
            Type propertyType = property.PropertyType;
            ConsoleView.PrintResponse($"Editing {property.Name} ({propertyType.Name})", ResponseStatus.Info);
            try
            {
                string input = ConsoleView.GetInput<string>($"Enter new value for {property.Name}:", "Invalid input");
                object? convertedValue = this.ConvertToType(input, propertyType);
                property.SetValue(obj, convertedValue);
                ConsoleView.PrintResponse("Value updated successfully!", ResponseStatus.Success);
            }
            catch (Exception ex)
            {
                ConsoleView.PrintResponse($"Error: {ex.Message}", ResponseStatus.Failure);
            }
        }

        private object? ConvertToType(string input, Type targetType)
        {
            if (targetType.IsEnum)
            {
                return Enum.Parse(targetType, input, true);
            }

            return Convert.ChangeType(input, targetType);
        }
    }
}
```


```
using System.Reflection;
using System.Reflection.Emit;

namespace Assignments
{
    /// <summary>
    /// Provides functionality to dynamically create a new type at runtime
    /// using Reflection.Emit, including fields, constructor, and methods.
    /// </summary>
    public class DynamicTypeBuilder
    {
        /// <summary>
        /// Builds and returns a dynamically generated type named "MatchStats".
        /// The type includes fields for team names and scores, a constructor
        /// to initialize them, and a method to determine the match result.
        /// </summary>
        /// <returns>The dynamically created MatchStats type.</returns>
        public Type? Execute()
        {
            AssemblyBuilder assemblyBuilder = AssemblyBuilder.DefineDynamicAssembly(new AssemblyName("Football"), AssemblyBuilderAccess.Run);

            ModuleBuilder moduleBuilder = assemblyBuilder.DefineDynamicModule("mainModule");

            TypeBuilder typeBuilder = moduleBuilder.DefineType("MatchStats", TypeAttributes.Public | TypeAttributes.Class);

            FieldBuilder teamA = typeBuilder.DefineField("TeamA", typeof(string), FieldAttributes.Public);
            FieldBuilder teamB = typeBuilder.DefineField("TeamB", typeof(string), FieldAttributes.Public);
            FieldBuilder scoreA = typeBuilder.DefineField("ScoreA", typeof(int), FieldAttributes.Public);
            FieldBuilder scoreB = typeBuilder.DefineField("ScoreB", typeof(int), FieldAttributes.Public);

            ConstructorBuilder constructorBuilder = typeBuilder.DefineConstructor(MethodAttributes.Public, CallingConventions.HasThis, new Type[] { typeof(string), typeof(string), typeof(int), typeof(int) });
            ILGenerator il = constructorBuilder.GetILGenerator();
            il.Emit(OpCodes.Ldarg_0);
            il.Emit(OpCodes.Call, typeof(object).GetConstructor(Type.EmptyTypes));

            il.Emit(OpCodes.Ldarg_0);
            il.Emit(OpCodes.Ldarg_1);
            il.Emit(OpCodes.Stfld, teamA);

            il.Emit(OpCodes.Ldarg_0);
            il.Emit(OpCodes.Ldarg_2);
            il.Emit(OpCodes.Stfld, teamB);

            il.Emit(OpCodes.Ldarg_0);
            il.Emit(OpCodes.Ldarg_3);
            il.Emit(OpCodes.Stfld, scoreA);

            il.Emit(OpCodes.Ldarg_0);
            il.Emit(OpCodes.Ldarg_S, (byte)4);
            il.Emit(OpCodes.Stfld, scoreB);

            il.Emit(OpCodes.Ret);

            MethodBuilder methodBuilder = typeBuilder.DefineMethod("GetWinnerDetails", MethodAttributes.Public, typeof(string), null);
            ILGenerator iL = methodBuilder.GetILGenerator();

            Label teamBLabel = iL.DefineLabel();
            Label drawLabel = iL.DefineLabel();

            MethodInfo? printWinner = typeof(string).GetMethod("Format", new Type[] { typeof(string), typeof(object) });
            MethodInfo? printDrawMessage = typeof(string).GetMethod("Format", new Type[] { typeof(string), typeof(object), typeof(object) });

            // if (ScoreA > ScoreB)
            iL.Emit(OpCodes.Ldarg_0);
            iL.Emit(OpCodes.Ldfld, scoreA);

            iL.Emit(OpCodes.Ldarg_0);
            iL.Emit(OpCodes.Ldfld, scoreB);

            iL.Emit(OpCodes.Ble_S, teamBLabel);

            // return TeamA Wins
            iL.Emit(OpCodes.Ldstr, "{0} Wins");
            iL.Emit(OpCodes.Ldarg_0);
            iL.Emit(OpCodes.Ldfld, teamA);
            iL.Emit(OpCodes.Box, typeof(string));
            iL.Emit(OpCodes.Call, printWinner);
            iL.Emit(OpCodes.Ret);

            // if ScoreB >= ScoreA
            iL.MarkLabel(teamBLabel);

            iL.Emit(OpCodes.Ldarg_0);
            iL.Emit(OpCodes.Ldfld, scoreB);

            iL.Emit(OpCodes.Ldarg_0);
            iL.Emit(OpCodes.Ldfld, scoreA);

            iL.Emit(OpCodes.Ble_S, drawLabel);

            // return TeamB Wins
            iL.Emit(OpCodes.Ldstr, "{0} Wins");
            iL.Emit(OpCodes.Ldarg_0);
            iL.Emit(OpCodes.Ldfld, teamB);
            iL.Emit(OpCodes.Box, typeof(string));
            iL.Emit(OpCodes.Call, printWinner);
            iL.Emit(OpCodes.Ret);

            iL.MarkLabel(drawLabel);

            iL.Emit(OpCodes.Ldstr, "Match Draw - Score {0} - {1}");

            iL.Emit(OpCodes.Ldarg_0);
            iL.Emit(OpCodes.Ldfld, scoreA);
            iL.Emit(OpCodes.Box, typeof(int));

            iL.Emit(OpCodes.Ldarg_0);
            iL.Emit(OpCodes.Ldfld, scoreB);
            iL.Emit(OpCodes.Box, typeof(int));

            iL.Emit(OpCodes.Call, printDrawMessage);
            iL.Emit(OpCodes.Ret);

            Type? matchStatsType = typeBuilder.CreateType();
            return matchStatsType;
        }
    }
}
```


```
using System;
using System.Reflection;
using System.Reflection.Emit;
using System.Text;

namespace Assignments
{
    /// <summary>
    /// Provides functionality to serialize objects into a json string format
    /// by dynamically generating and executing IL code using Reflection.Emit.
    /// </summary>
    public class EmitSerializer
    {
        /// <summary>
        /// Serializes the given object into a string representation by generating a dynamic method at runtime.
        /// </summary>
        /// <param name="obj">The object to serialize.</param>
        /// <returns>A string representation of the object's properties and values.</returns>
        public string Serialize(object obj)
        {
            Type type = obj.GetType();
            return this.GenerateAndExecuteSerializer(type, obj);
        }

        private string GenerateAndExecuteSerializer(Type type, object obj)
        {
            DynamicMethod method = new DynamicMethod("Serialize" + type.Name, typeof(string), new Type[] { typeof(object) }, true);
            MethodInfo? stringBuilderAppendMethod = typeof(StringBuilder).GetMethod("Append", new[] { typeof(string) });
            ILGenerator il = method.GetILGenerator();

            il.DeclareLocal(typeof(StringBuilder));
            il.DeclareLocal(type);

            // StringBuilder stringBuilder = new StringBuilder();
            il.Emit(OpCodes.Newobj, typeof(StringBuilder).GetConstructor(Type.EmptyTypes));
            il.Emit(OpCodes.Stloc_0);

            // casting obj to type T.
            il.Emit(OpCodes.Ldarg_0);
            il.Emit(OpCodes.Castclass, type);
            il.Emit(OpCodes.Stloc_1);

            // stringBuilder.Append("{");
            il.Emit(OpCodes.Ldloc_0);
            il.Emit(OpCodes.Ldstr, "{");
            il.Emit(OpCodes.Callvirt, stringBuilderAppendMethod);
            il.Emit(OpCodes.Pop);

            PropertyInfo[] properties = type.GetProperties();

            for (int i = 0; i < properties.Length; i++)
            {
                PropertyInfo property = properties[i];

                // stringBuilder.Append("\"PropName\": \"");
                il.Emit(OpCodes.Ldloc_0);
                il.Emit(OpCodes.Ldstr, $"\"{property.Name}\": \"");
                il.Emit(OpCodes.Callvirt, stringBuilderAppendMethod);
                il.Emit(OpCodes.Pop);

                // stringBuilder.Append(value.ToString())
                il.Emit(OpCodes.Ldloc_0);
                il.Emit(OpCodes.Ldloc_1);
                il.Emit(OpCodes.Callvirt, property.GetGetMethod());

                if (property.PropertyType.IsValueType)
                {
                    il.Emit(OpCodes.Box, property.PropertyType);
                }

                il.Emit(OpCodes.Callvirt, typeof(object).GetMethod("ToString"));
                il.Emit(OpCodes.Callvirt, stringBuilderAppendMethod);
                il.Emit(OpCodes.Pop);

                // stringBuilder.Append("\"");
                il.Emit(OpCodes.Ldloc_0);
                il.Emit(OpCodes.Ldstr, "\"");
                il.Emit(OpCodes.Callvirt, stringBuilderAppendMethod);
                il.Emit(OpCodes.Pop);

                if (i < properties.Length - 1)
                {
                    il.Emit(OpCodes.Ldloc_0);
                    il.Emit(OpCodes.Ldstr, ", ");
                    il.Emit(OpCodes.Callvirt, stringBuilderAppendMethod);
                    il.Emit(OpCodes.Pop);
                }
            }

            // stringBuilder.Append("}");
            il.Emit(OpCodes.Ldloc_0);
            il.Emit(OpCodes.Ldstr, "}");
            il.Emit(OpCodes.Callvirt, stringBuilderAppendMethod);
            il.Emit(OpCodes.Pop);

            il.Emit(OpCodes.Ldloc_0);
            il.Emit(OpCodes.Callvirt, typeof(object).GetMethod("ToString"));
            il.Emit(OpCodes.Ret);

            return (string)method.Invoke(null, new object[] { obj });
        }
    }
}
```


```
using System;
using System.Reflection;
using System.Reflection.Emit;

namespace Assignments
{
    /// <summary>
    /// Provides functionality to dynamically generate mock implementations
    /// of interfaces at runtime using Reflection.Emit.
    /// </summary>
    public class MockBuilder
    {
        /// <summary>
        /// Creates a mock object for the specified interface type.
        /// The generated mock implements all interface methods and returns default values.
        /// </summary>
        /// <typeparam name="T">The interface type to mock.</typeparam>
        /// <returns>An instance of a dynamically generated mock implementation.</returns>
        public T CreateMock<T>()
        {
            Type interfaceType = typeof(T);

            AssemblyName assemblyName = new AssemblyName("DynamicMockAssembly");
            AssemblyBuilder assemblyBuilder = AssemblyBuilder.DefineDynamicAssembly(assemblyName, AssemblyBuilderAccess.Run);
            ModuleBuilder moduleBuilder = assemblyBuilder.DefineDynamicModule("MainModule");
            TypeBuilder typeBuilder = moduleBuilder.DefineType(interfaceType.Name + "Mock", TypeAttributes.Public | TypeAttributes.Class);

            typeBuilder.AddInterfaceImplementation(interfaceType);

            foreach (MethodInfo method in interfaceType.GetMethods())
            {
                this.CreateMethod(typeBuilder, method);
            }

            Type? mockType = typeBuilder.CreateType();

            return (T)Activator.CreateInstance(mockType);
        }

        private void CreateMethod(TypeBuilder typeBuilder, MethodInfo interfaceMethod)
        {
            ParameterInfo[] parameters = interfaceMethod.GetParameters();
            Type[] parameterTypes = new Type[parameters.Length];

            for (int i = 0; i < parameters.Length; i++)
            {
                parameterTypes[i] = parameters[i].ParameterType;
            }

            MethodBuilder methodBuilder = typeBuilder.DefineMethod(interfaceMethod.Name, MethodAttributes.Public | MethodAttributes.Virtual, interfaceMethod.ReturnType, parameterTypes);
            ILGenerator il = methodBuilder.GetILGenerator();
            this.DefineOpcodeForDefaultValue(il, interfaceMethod.ReturnType);
            il.Emit(OpCodes.Ret);
            typeBuilder.DefineMethodOverride(methodBuilder, interfaceMethod);
        }

        private void DefineOpcodeForDefaultValue(ILGenerator il, Type returnType)
        {
            if (returnType == typeof(void))
            {
                return;
            }

            if (returnType.IsValueType)
            {
                LocalBuilder instance = il.DeclareLocal(returnType);
                il.Emit(OpCodes.Ldloca_S, instance);
                il.Emit(OpCodes.Initobj, returnType);
                il.Emit(OpCodes.Ldloc, instance);
            }
            else
            {
                il.Emit(OpCodes.Ldnull);
            }
        }
    }
}
```


```
namespace PlayerStatsPlugin
{
    /// <summary>
    /// Represents data for a football player, including performance metrics
    /// such as matches played, goals, and assists.
    /// </summary>
    public class PlayerStats
    {
        /// <summary>
        /// The unique identifier of the player.
        /// </summary>
        public int PlayerId;

        private DateTime _lastUpdated;

        /// <summary>
        /// Initializes a new instance of the <see cref="PlayerStats"/> class
        /// with player details and performance statistics.
        /// </summary>
        /// <param name="playerId">The unique identifier of the player.</param>
        /// <param name="lastUpdated">The last updated timestamp of the stats.</param>
        /// <param name="name">The name of the player.</param>
        /// <param name="matchesPlayed">Total number of matches played.</param>
        /// <param name="goals">Total number of goals scored.</param>
        /// <param name="assists">Total number of assists made.</param>
        public PlayerStats(int playerId, DateTime lastUpdated, string name, int matchesPlayed, int goals, int assists)
        {
            this.PlayerId = playerId;
            this._lastUpdated = lastUpdated;
            this.Name = name;
            this.MatchesPlayed = matchesPlayed;
            this.Goals = goals;
            this.Assists = assists;
        }

        /// <summary>
        /// Event triggered when the player's statistics are updated.
        /// </summary>
        public event Action? OnStatsUpdated;

        /// <summary>
        /// Gets or sets the name of the player.
        /// </summary>
        /// <value>The player's full name.</value>
        public string Name { get; set; }

        /// <summary>
        /// Gets or sets the number of matches played by the player.
        /// </summary>
        /// <value>The total matches played.</value>
        public int MatchesPlayed { get; set; }

        /// <summary>
        /// Gets or sets the number of goals scored by the player.
        /// </summary>
        /// <value>The total goals scored.</value>
        public int Goals { get; set; }

        /// <summary>
        /// Gets or sets the number of assists made by the player.
        /// </summary>
        /// <value>The total assists made.</value>
        public int Assists { get; set; }

        /// <summary>
        /// Calculates the goal-to-match ratio for the player.
        /// </summary>
        /// <returns>
        /// The ratio of goals scored to matches played. Returns 0 if no matches were played.
        /// </returns>
        public double CalculateGoalRatio()
        {
            return this.MatchesPlayed == 0 ? 0 : (double)this.Goals / this.MatchesPlayed;
        }

        /// <summary>
        /// Displays a summary of the player's goals and assists.
        /// </summary>
        public void ShowSummary()
        {
            Console.WriteLine($"{this.Name}: {this.Goals} Goals, {this.Assists} Assists");
        }

        /// <summary>
        /// Updates the player's goals and assists, logs the update, and triggers the OnStatsUpdated event.
        /// </summary>
        /// <param name="goals">The updated number of goals.</param>
        /// <param name="assists">The updated number of assists.</param>
        public void UpdateStats(int goals, int assists)
        {
            this.Goals = goals;
            this.Assists = assists;

            this.LogUpdate();

            this.OnStatsUpdated?.Invoke();
        }

        private void LogUpdate()
        {
            Console.WriteLine("Stats updated successfully.");
        }
    }
}

```


```
using System.Reflection;
using System.Reflection.Emit;
using System.Text;

namespace Assignments
{
    /// <summary>
    /// Provides a simple serialization mechanism using Reflection to convert an object's public properties into a string format.
    /// </summary>
    public class Serializer
    {
        /// <summary>
        /// Serializes the given object into a string representation by reading its public properties using Reflection.
        /// </summary>
        /// <param name="obj">The object to serialize.</param>
        /// <returns>
        /// A string containing the serialized representation of the object in a key-value format.
        /// </returns>
        public string Serialize(object obj)
        {
            StringBuilder stringBuilder = new StringBuilder();
            Type type = obj.GetType();
            stringBuilder.Append("{");

            PropertyInfo[] properties = type.GetProperties();
            for (int i = 0; i < properties.Length; i++)
            {
                PropertyInfo property = properties[i];
                object? value = property.GetValue(obj);
                stringBuilder.Append($"\"{property.Name}\": \"{value}\"");
                if (i < properties.Length - 1)
                {
                    stringBuilder.Append(", ");
                }
            }

            stringBuilder.Append("}");
            return stringBuilder.ToString();
        }
    }
}
```


```
/// <summary>
/// Represents the list of available reflection tasks in the application.
/// </summary>
public enum Tasks
{
    /// <summary>
    /// Inspect assembly metadata such as types, methods, properties, fields, and events.
    /// </summary>
    Task1 = 1,

    /// <summary>
    /// Dynamically inspect and modify object properties at runtime.
    /// </summary>
    Task2,

    /// <summary>
    /// Dynamically invoke methods on an object using reflection.
    /// </summary>
    Task3,

    /// <summary>
    /// Build a new type dynamically at runtime using Reflection.Emit.
    /// </summary>
    Task4,

    /// <summary>
    /// Implement a plugin system that loads and executes external assemblies.
    /// </summary>
    Task5,

    /// <summary>
    /// Create a mocking framework that generates mock objects dynamically.
    /// </summary>
    Task6,

    /// <summary>
    /// Implement a serializer using Reflection and optimize it using Reflection.Emit.
    /// </summary>
    Task7,
}
```


```
/// <summary>
/// Provides a short description for each task to display in the menu.
/// </summary>
/// <param name="task">The selected task.</param>
/// <returns>A brief description of the task.</returns>
public static string GetTaskDescription(Tasks task)
{
    return task switch
    {
        Tasks.Task1 => "Inspect assembly metadata (types, methods, properties, fields, events).",
        Tasks.Task2 => "Inspect and modify object properties dynamically.",
        Tasks.Task3 => "Invoke methods dynamically using reflection.",
        Tasks.Task4 => "Create types at runtime using Reflection.Emit.",
        Tasks.Task5 => "Load and execute plugins dynamically.",
        Tasks.Task6 => "Generate mock objects dynamically for testing.",
        Tasks.Task7 => "Serialize objects using Reflection and optimize with Emit.",
        _ => "Unknown task"
    };
}
```