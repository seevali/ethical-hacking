# Deciphering a message using monoalphabetic substitution cipher - Task 02

## Challenge

### Ciphertext

> BEYRWE WEHRWLSDP XTHC HRDYEXXSRD IJPSXKWJKE HJD EQMOJSD KR MEWXRD IJZSDP SK  KCJK CE SX DRK BRTDL KR IJZE JDA HRDYEXXSRD JDL KCJK SY CE LREX SK ISPCK BE TXEL JPJSD JX EUSLEDHE JPJSDXK CSI

## Solution

### Decipher (Plain/Decrypted) Text

> 

### Alphabets

	

## Cryptanalysis (Breaking the secret)

### Python script to find letter frequency in a text
	
	>>>import collections
	>>>print collections.Counter("BEYRWE WEHRWLSDP XTHC HRDYEXXSRD IJPSXKWJKE HJD EQMOJSD KR MEWXRD IJZSDP SK  KCJK CE SX DRK BRTDL KR IJZE JDA HRDYEXXSRD JDL KCJK SY CE LREX SK ISPCK BE TXEL JPJSD JX EUSLEDHE JPJSDXK CSI")

### Result of the script

> 'E': 17, 'D': 16, 'J': 15, 'S': 15, 'K': 13, 'R': 12, 'X': 12, 'C': 7, 'H': 6, 'L': 6, 'P': 6, 'I': 5, 'W': 5, 'Y': 4, 'B': 3, 'T': 3, 'M': 2, 'Z': 2, 'A': 1, 'O': 1, 'Q': 1, 'U': 1

### Step 01 : Finding the occurences of most frequent 3 letters with other letters

      A B C D E F G H I J K L M N O P Q R S T U V W X Y Z 	Appears	  Avoids                Possibilities
	E 0 2 2 1 0 0 0 2 0 0 1 2 1 0 0 0 1 1 0 0 1 0 3 4 2 1   14        12	<= Vowel        a/e/i
	D 1 0 0 0 1 0 0 1 0 1 0 2 0 0 0 2 0 6 5 1 0 0 0 1 2 0   11        15	<= V/C ?        a/e/i/t/n		RD ^| SD ^|
	J 0 0 2 3 0 0 0 1 3 0 3 0 0 0 1 5 0 0 3 0 0 0 1 1 0 2   11        15	<= V/C ?    	a/e/i/t/n 		JD ^| IJ ^| JK ^|


	BEYRWE WEHRWLSDP XTHC HRDYEXXSRD IJPSXKWJKE HJD EQMOJSD KR MEWXRD IJZSDP SK  KCJK CE SX DRK BRTDL KR IJZE JDA HRDYEXXSRD JDL KCJK SY CE LREX SK ISPCK BE TXEL JPJSD JX EUSLEDHE JPJSDXK CSI

### Step 02 : Repeating Letters
