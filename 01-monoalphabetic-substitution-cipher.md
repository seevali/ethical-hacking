# Deciphering a message using monoalphabetic substitution cipher

## Challenge

### Ciphertext

> KIVEVL XNJV INSLVE VLWPNLE NMORF XNJTLW FOO ARCX COLZTEVLCV NXVNE OZ FXVTS IOSPE CRB HRNSFVS ZTLNP OL KNFRSENY FXV IOSPE CRB HRNSFVS ZTLNPK WVF RLEVSINY OL ZSTENY ITFX FIO OZ FXV KVAT ZTLNPTKFK FO MV EVCTEVE FOENY

## Solution

### Decipher (Plain/Decrypted) Text

> sweden have warned england about having too much confidence ahead of their world cup quarter final on saturday the world cup quarter finals get underway on friday with two of the semi finalists to be decided today


### Alphabets

	Plaintext	A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
	Ciphertext	m p c   d t   q w v s n b a o l   u r i   e g h y f



## Cryptanalysis (Breaking the secret)


### Python script to find letter frequency in a text

	>>>import collections
	>>>print collections.Counter("KIVEVL XNJV INSLVE VLWPNLE NMORF XNJTLW FOO ARCX COLZTEVLCV NXVNE OZ FXVTS IOSPE CRB HRNSFVS ZTLNP OL KNFRSENY FXV IOSPE CRB HRNSFVS ZTLNPK WVF RLEVSINY OL ZSTENY ITFX FIO OZ FXV KVAT ZTLNPTKFK FO MV EVCTEVE FOENY")


### Result of the script

> 'V': 19, 'N': 17, 'E': 14, 'F': 14, 'L': 13, 'O': 13, 'S': 11, 'T': 11, 'R': 8, 'X': 8, 'I': 7, 'Z': 7, 'C': 6, 'K': 6, 'P': 6, 'Y': 4, 'W': 3, 'A': 2, 'B': 2, 'H': 2, 'J': 2, 'M': 2

### Step 01 : Finding the occurences of most frequent 3/4 letters with other letters

      A B C D E F G H I J K L M N O P Q R S T U V W X Y Z 	Appears	  Avoids                Possibilities
	V 1 0 1 0 8 3 0 0 1 1 1 4 1 1 0 0 0 0 3 1 0 0 1 4 0 0   14        12	<= Vowel        a/e/i
	N 0 0 0 0 4 1 0 0 2 2 1 4 1 0 0 4 0 2 3 0 0 1 0 2 4 0   13        13	<= Vowel        a/e/i
	E 0 0 0 0 0 0 0 0 0 0 0 2 0 3 1 2 0 0 1 3 0 8 0 0 0 0   7         19	<= Consonant    t/n/s/h/r/d
	F 0 0 0 0 0 0 0 0 1 0 2 0 0 0 3 0 0 2 2 1 0 3 0 4 0 0   8         18	<= Consonant    t/n/s/h/r/d

### Step 02 : Repeating Letters

	OO => ss,ee,tt,ff,ll,mm,oo

	FOO => ?ss => OL/OZ are confusing
	FOO => ?ee => OL/OZ are confusing
	FOO => ?tt => OL/OZ are confusing
	FOO => ?ff => OL/OZ are confusing
	FOO => ?ll => OL/OZ are confusing
	FOO => ?mm => OL/OZ/FO are confusing
	FOO => ?00 => FOO may be 'too' and OL/OZ may be 'of' on' 
	We can assume 'O' => 'o'

#### ALPHABET
	Plaintext	A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
	Ciphertext	                            o

#### Solution 01 : Replace 'O' with 'o'

> KIVEVL XNJV INSLVE VLWPNLE NMoRF XNJTLW Foo ARCX CoLZTEVLCV NXVNE oZ FXVTS IoSPE CRB HRNSFVS ZTLNP oL KNFRSENY FXV IoSPE CRB HRNSFVS ZTLNPK WVF RLEVSINY oL ZSTENY ITFX FIo oZ FXV KVAT ZTLNPTKFK Fo MV EVCTEVE FoENY

### Step 03 : Working on 'Foo'
	
	Only possible words are 'too' and 'zoo'

	If 'F' => 'z'
		'Fo' => 'zo' doesn't give any meaning.
	If 'F' => 't'
		'Fo' => 'to' is ok

#### ALPHABET
	Plaintext	A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
	Ciphertext	          t                 o

#### Solution 02 : Replace 'F' with 't'

> KIVEVL XNJV INSLVE VLWPNLE NMoRt XNJTLW too ARCX CoLZTEVLCV NXVNE oZ tXVTS IoSPE CRB HRNStVS ZTLNP oL KNtRSENY tXV IoSPE CRB HRNStVS ZTLNPK WVt RLEVSINY oL ZSTENY ITtX tIo oZ tXV KVAT ZTLNPTKtK to MV EVCTEVE toENY

### Step 04 : What is this 'tIo'?
	
	Only available possibilities are,

	tao/tho/too/two ('two' is added after Step 08)

	'too' <= not possible (O => o)
	'tao' <= senseless

	'tIo' => tho (In Step 08 it was found that this is wrong [previously assumed])

	*** This may be wrong *** (<= previously assumed)

	*** Coreect replacement is

	I => w

#### ALPHABET
	Plaintext	A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
	Ciphertext	          t     w           o

#### Solution 03 : Replace 'I' with 'w' (Corrected after Step 08)

> KwVEVL XNJV wNSLVE VLWPNLE NMoRt XNJTLW too ARCX CoLZTEVLCV NXVNE oZ tXVTS woSPE CRB HRNStVS ZTLNP oL KNtRSENY tXV woSPE CRB HRNStVS ZTLNPK WVt RLEVSwNY oL ZSTENY wTtX two oZ tXV KVAT ZTLNPTKtK to MV EVCTEVE toENY

### Step 05 : What is this 'toENY'

	Most suitable 5 letter word starting with 'to' is,

	'today'

	E => d
	N => a
	Y => y

#### ALPHABET
	Plaintext	A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
	Ciphertext	        d t     w         a o                   y  

#### Solution 04 I : Replace 'E' with 'd'

> KwVdVL XNJV wNSLVd VLWPNLd NMoRt XNJTLW too ARCX CoLZTdVLCV NXVNd oZ tXVTS woSPd CRB HRNStVS ZTLNP oL KNtRSdNY tXV woSPd CRB HRNStVS ZTLNPK WVt RLdVSwNY oL ZSTdNY wTtX two oZ tXV KVAT ZTLNPTKtK to MV dVCTdVd todNY

#### Solution 04 II : Replace 'N' with 'a'

> KwVdVL XaJV waSLVd VLWPaLd aMoRt XaJTLW too ARCX CoLZTdVLCV aXVad oZ tXVTS woSPd CRB HRaStVS ZTLaP oL KatRSdaY tXV woSPd CRB HRaStVS ZTLaPK WVt RLdVSwaY oL ZSTdaY wTtX two oZ tXV KVAT ZTLaPTKtK to MV dVCTdVd todaY

#### Solution 04 III : Replace 'Y' with 'y'

> KwVdVL XaJV waSLVd VLWPaLd aMoRt XaJTLW too ARCX CoLZTdVLCV aXVad oZ tXVTS woSPd CRB HRaStVS ZTLaP oL KatRSday tXV woSPd CRB HRaStVS ZTLaPK WVt RLdVSway oL ZSTday wTtX two oZ tXV KVAT ZTLaPTKtK to MV dVCTdVd today

### Step 06 : What is this 'tXV'

	This may be 

	the/tea/ten/til/tip/top/try/two

	** We can discard 'top' and 'two' as 'O' => 'o'
	** We can discard 'try' as 'Y' => 'y'

	** 'the' may be the most suitable word. If so,

	X => h
	V => e <= In Step 01 we assumed that 'V' should be a vowel and may be a/e/i

#### ALPHABET
	Plaintext	A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
	Ciphertext	        d t     w         a o             e   h y 

#### Solution 05 I : Replace 'X' with 'h'

> KwVdVL haJV waSLVd VLWPaLd aMoRt haJTLW too ARCh CoLZTdVLCV ahVad oZ thVTS woSPd CRB HRaStVS ZTLaP oL KatRSday thV woSPd CRB HRaStVS ZTLaPK WVt RLdVSway oL ZSTday wTth two oZ thV KVAT ZTLaPTKtK to MV dVCTdVd today

#### Solution 05 II : Replace 'V' with 'e'

> KwedeL haJe waSLed eLWPaLd aMoRt haJTLW too ARCh CoLZTdeLCe ahead oZ theTS woSPd CRB HRaSteS ZTLaP oL KatRSday the woSPd CRB HRaSteS ZTLaPK Wet RLdeSway oL ZSTday wTth two oZ the KeAT ZTLaPTKtK to Me deCTded today

### Step 07 : What is this 'to Me'
	
	It may be => 'to be'

	M => b

#### ALPHABET
	Plaintext	A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
	Ciphertext	        d t     w       b a o             e   h y 

#### Solution 06 : Replace 'M' with 'b'
	
> KwedeL haJe waSLed eLWPaLd aboRt haJTLW too ARCh CoLZTdeLCe ahead oZ theTS woSPd CRB HRaSteS ZTLaP oL KatRSday the woSPd CRB HRaSteS ZTLaPK Wet RLdeSway oL ZSTday wTth two oZ the KeAT ZTLaPTKtK to be deCTded today

### Step 08 : What is this 'to be deCTded'

	It may be => 'to be decided'

	C => c
	T => i

#### ALPHABET
	Plaintext	A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
	Ciphertext	    c   d t     w       b a o         i   e   h y 

#### Solution 07 I : Replace 'C' with 'c'
	
> KwedeL haJe waSLed eLWPaLd aboRt haJTLW too ARch coLZTdeLce ahead oZ theTS woSPd cRB HRaSteS ZTLaP oL KatRSday the woSPd cRB HRaSteS ZTLaPK Wet RLdeSway oL ZSTday wTth two oZ the KeAT ZTLaPTKtK to be decTded today

#### Solution 07 II : Replace 'T' with 'i'
	
> KwedeL haJe waSLed eLWPaLd aboRt haJiLW too ARch coLZideLce ahead oZ theiS woSPd cRB HRaSteS ZiLaP oL KatRSday the woSPd cRB HRaSteS ZiLaPK Wet RLdeSway oL ZSiday with two oZ the KeAi ZiLaPiKtK to be decided today

### Step 09 : 'ahead oZ' and 'with two oZ the'

	We can safely assume that 'oZ' => 'of'

	Z => f

#### ALPHABET
	Plaintext	A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
	Ciphertext	    c   d t     w       b a o         i   e   h y f

#### Solution 08 : Replace 'Z' with 'f'

> KwedeL haJe waSLed eLWPaLd aboRt haJiLW too ARch coLfideLce ahead of theiS woSPd cRB HRaSteS fiLaP oL KatRSday the woSPd cRB HRaSteS fiLaPK Wet RLdeSway oL fSiday with two of the KeAi fiLaPiKtK to be decided today

### Step 10 : 'oL fSiday'

	Is this => 'on friday' ?

	L => n
	S => r

#### ALPHABET
	Plaintext	A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
	Ciphertext	    c   d t     w     n b a o       r i   e   h y f

#### Solution 09 I : Replace 'L' with 'n'

> Kweden haJe waSned enWPand aboRt haJinW too ARch confidence ahead of theiS woSPd cRB HRaSteS finaP on KatRSday the woSPd cRB HRaSteS finaPK Wet RndeSway on fSiday with two of the KeAi finaPiKtK to be decided today

#### Solution 09 II : Replace 'S' with 'r'

> Kweden haJe warned enWPand aboRt haJinW too ARch confidence ahead of their worPd cRB HRarter finaP on KatRrday the worPd cRB HRarter finaPK Wet Rnderway on friday with two of the KeAi finaPiKtK to be decided today

### Step 11: 'Kweden'

	Is this => 'sweden' ?

	K => s

#### ALPHABET
	Plaintext	A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
	Ciphertext	    c   d t     w   s n b a o       r i   e   h y f

#### Solution 10 : Replace 'K' with 's'

> sweden haJe warned enWPand aboRt haJinW too ARch confidence ahead of their worPd cRB HRarter finaP on satRrday the worPd cRB HRarter finaPs Wet Rnderway on friday with two of the seAi finaPists to be decided today

### Step 12 : 'aboRt'

	Is this => 'about' ?

	R => u

#### ALPHABET
	Plaintext	A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
	Ciphertext	    c   d t     w   s n b a o     u r i   e   h y f

#### Solution 11 : Replace 'R' with 'u'

> sweden haJe warned enWPand about haJinW too Auch confidence ahead of their worPd cuB Huarter finaP on saturday the worPd cuB Huarter finaPs Wet underway on friday with two of the seAi finaPists to be decided today

### Step 13 : 'enWPand about haJinW too Auch confidence'

	Is this => 'england about having too much confidence' ?

	W => g
	P => l
	J => v
	A => m

#### ALPHABET
	Plaintext	A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
	Ciphertext	m   c   d t     w v s n b a o l   u r i   e g h y f

#### Solution 12 I : Replace 'W' with 'g'

> sweden haJe warned engPand about haJing too Auch confidence ahead of their worPd cuB Huarter finaP on saturday the worPd cuB Huarter finaPs get underway on friday with two of the seAi finaPists to be decided today

#### Solution 12 II : Replace 'P' with 'l'

> sweden haJe warned england about haJing too Auch confidence ahead of their world cuB Huarter final on saturday the world cuB Huarter finals get underway on friday with two of the seAi finalists to be decided today

#### Solution 12 III : Replace 'J' with 'v'

> sweden have warned england about having too Auch confidence ahead of their world cuB Huarter final on saturday the world cuB Huarter finals get underway on friday with two of the seAi finalists to be decided today

#### Solution 12 IV : Replace 'A' with 'm'

> sweden have warned england about having too much confidence ahead of their world cuB Huarter final on saturday the world cuB Huarter finals get underway on friday with two of the semi finalists to be decided today

### Step 14 : 'world cuB Huarter final'

	Is this => 'world cup quarter final' ?

	B => p
	H => q

#### ALPHABET
	Plaintext	A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
	Ciphertext	m p c   d t   q w v s n b a o l   u r i   e g h y f

### Solution 13 I : Replace 'B' with 'p'

> sweden have warned england about having too much confidence ahead of their world cup Huarter final on saturday the world cup Huarter finals get underway on friday with two of the semi finalists to be decided today

#### Solution 13 II : Replace 'H' with 'q'

> sweden have warned england about having too much confidence ahead of their world cup quarter final on saturday the world cup quarter finals get underway on friday with two of the semi finalists to be decided today
