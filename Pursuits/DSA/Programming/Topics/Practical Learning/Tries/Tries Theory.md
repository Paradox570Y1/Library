- `Trie` data structure is used if you want to create some structure for storing words and searching in that structure some particular word or prefix of that particular word.
	![[Pasted image 20251001152013.png]]
- It's a struct or class which has two member variable which are:
	- array of class type and size 26
	- boolean flag - used to depict the ending of a word in trie data structure.
- It is like a Search Tree with 26 children at a high level.
	![[Pasted image 20251218202554.png|400]]


# Process

- Start traversing the word and for every word starting point will be root of Trie.
- If word exists then go to the reference it stores else create a new reference at it's position and then go to that reference.
- If you have reached the end of a word then  while creating new reference change the flag to `True` to indicate the ending of that word.
![[Pasted image 20251001153949.png|400]]

- Now in this Trie structure you can check the word as well as prefix of the word.

# Uses
- search
- starts with
- Used in auto complete
- Used in networking for IP prefix check - subnet.
- browser search

# More about tries
- It can be extremely dense especially in case invalid words are allowed.
- The depth of tries is O(h) in case of english valid words where longest word is about 45 characters (==**[pneumonoultramicroscopicsilicovolcanoconiosis](https://www.google.com/search?q=pneumonoultramicroscopicsilicovolcanoconiosis&sca_esv=0ccf53d8b4904cec&rlz=1C1RXQR_enIN1060IN1060&ei=PiFEaeygONianesP1_DK2A0&oq=biggest+valid+word+in+e&gs_lp=Egxnd3Mtd2l6LXNlcnAiF2JpZ2dlc3QgdmFsaWQgd29yZCBpbiBlKgIIADIFECEYoAEyBRAhGKABMgUQIRigATIFECEYoAEyBRAhGJ8FSPk5ULYHWOwucAp4AZABAJgBoAGgAbsQqgEEMC4xNbgBA8gBAPgBAZgCGaACpxHCAgoQABhHGNYEGLADwgILEAAYgAQYigUYkQLCAgUQABiABMICBRAuGIAEwgIHEAAYgAQYCsICBhAAGBYYHsICCBAAGBYYHhgKwgILEAAYgAQYigUYhgPCAggQABiABBiiBMICBRAAGO8FwgIIEAAYiQUYogSYAwCIBgGQBgiSBwUxMC4xNaAH5EyyBwQwLjE1uAeBEcIHBzAuMTUuMTDIB0aACAE&sclient=gws-wiz-serp&mstk=AUtExfBcYE-5w3EuADEmla7hqHerVvw8MhiUxRn5WpiFiWuWyExR0hWYilVbQ6hoIeR-8y3d4GLpzYn9MGtzK9DW6RSlzbu62XvBLz9LpAnAy-atVFDtjZOWX8vzk7093eDWBbKPnFkmGVFMn6Ztq68FPjxus2QMZ43yBaBDxSjOWFjsl0PVjg_ETdCN-PrEMeDFYonI&csui=3&ved=2ahUKEwi5o4OpvceRAxXhe2wGHQJfCOgQgK4QegQIARAC)**== )then that's the maximum depth. But if we are just storing words even invalid ones then it can go upto O(N).
- Negative point is high memory footprint.
- CRUD + startsWith cost - O (max valid key)

# Implementation
![[Pasted image 20251218211006.png|300]]

![[Pasted image 20251218211324.png|300]]

![[Pasted image 20251218211958.png|300]]
- Deletion can be soft delete or deleting each letter.
	- In soft delete we just mark the value null and structure of word persists.
		- This will lead to wastage of search compute as it will traverse through the characters in soft deleted words as well just to find no value.
	- In hard delete we delete the node which does not have children and has no value.
