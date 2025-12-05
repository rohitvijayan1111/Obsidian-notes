
![[Pasted image 20251205123037.png]]

![[Pasted image 20251205123043.png]]

head usually refer to a branch reference not a commit


use>  git switch master/checkout master to reattach the head


You can go in point in time, to some commit and create a new branch, now the head isnt detached rather pointing to this head(using switch -c)


![[Pasted image 20251205124112.png]]



git switch -

-> when during detached, head, it will take the head, to the branch we wre reccently on


---


![[Pasted image 20251205125319.png]]
	``Git checkout HEAD <file> or git checkout -- <file>``
it would remove the committed changes in the file, to what was there in the previous commit.

QUestions?
What if we have stagged changes? at that time also will it move back in time

---- 

![[Pasted image 20251205125352.png]]
![[Pasted image 20251205125426.png]]
![[Pasted image 20251205125511.png]]
![[Pasted image 20251205125745.png]]
will the changes will be still there in the working directory or will it be removed from there s well?
it will just removed from the stagged, not deleted
