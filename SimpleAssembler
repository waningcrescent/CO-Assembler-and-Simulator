mydict = {'add': '10000' , 'sub': '10001' , 'mov1': '10010' , 'mov2': '10011', 'ld': '10100', 'st': '10101' , 'mul': '10110' , 'div': '10111' , 'rs': '11000' , 'ls': '11001' , 'xor': '11010' , 'or': '11011' , 'and': '11100' , 'not': '11101' , 'cmp': '11110' , 'jmp': '11111', 'jlt': '01100', 'jgt': '01101' , 'je': '01111' , 'hlt': '01010' }
registers =  {'R0': '000' , 'R1': '001', 'R2': '010' , 'R3': '011', 'R4': '100' , 'R5': '101', 'R6': '110' , 'FLAGS': '111' }
labels = {}
variables = []
type = { 'add' : 'A' , 'sub' : 'A' , 'mul' : 'A', 'xor': 'A', 'or': 'A', 'and': 'A', 'mov1': 'B', 'rs' : 'B', 'ls': 'B', 'mov2': 'C', 'div': 'C', 'not': 'C', 'cmp': 'C', 'ld': 'D', 'st': 'D', 'jmp': 'E', 'jlt': 'E', 'jgt': 'E', 'je': 'E' , 'hlt' : 'F'}
labelrepeat=[]
st=""
v=0 
import sys

print('\n')
l1=[]
f1=sys.stdin.readlines()
ct=0
ct1=[]
lab1=[]
for lines in f1:
    if lines!="\n":
        z=lines.split()
        word=z[0]
        if word[len(z[0])-1:]==":":
            if z[0].replace(":","") not in lab1:
                lab1.append(z[0].replace(":","")) 
                ct1.append(ct)
            else:
                labelrepeat.append(z[0].replace(":",""))
        if word=="var" or (word.replace(":","") in lab1 and len(z)==1):
            pass
        else:
            ct+=1
ct2=ct

labels=dict(zip(lab1,ct1))
def funcA(lst):
    strA=""
    try:
        len(lst)==4
        if lst[1] in registers.keys() :
            if lst[2] in registers.keys() :
                if lst[3] in registers.keys():
                    opcode = mydict.get(lst[0])
                    unused = '00'
                    reg1 = registers.get(lst[1])
                    reg2 = registers.get(lst[2])
                    reg3 = registers.get(lst[3])
                    strA =  opcode + unused + reg1 + reg2 + reg3
                    print(strA)
                else:
                    print("ERROR: Register(s) not found")
    except:
        print('ERROR: Instruction not in ISA')


def funcB(lst):
    try:
        len(lst) == 3
        if lst[1] in registers.keys():
            strB = ''
            opcode = mydict.get(lst[0])
            reg1 = registers.get(lst[1])
            try:
                imm = lst[2]
                imm = imm[1:]
                dec = int(imm)
                if 0 <= dec <= 255:
                    e=str(bin(dec))
                    e=e[2:]
                    l=len(e)
                    imm = ((8-l)*"0"+e)
                    strB = opcode + reg1 + imm
                    print(strB)
                else : 
                    print("ERROR: Illegal Immediate Values (More than 8 bits)")
            except ValueError:
                print("ERROR: Invalid literal for Immediate")

        else:
            print("ERROR: Register not found")
    except:
        print('ERROR: Instruction not in ISA')


def funcC(lst):
    try:
        len(lst) == 3
        if lst[1] in registers.keys() and lst[2] in registers.keys():
            strC = ''
            opcode = mydict.get(lst[0])
            unused = '00000'
            reg1 = registers.get(lst[1])
            reg2 = registers.get(lst[2])
            strC = opcode + unused + reg1 + reg2
            print(strC)
        else:
            print("ERROR: Register(s) not found")
    except:
        print('ERROR: Instruction not in ISA')
    

def funcD(lst):
    try:
        len(lst) == 3
        if lst[1] in registers.keys():
            strD = ''
            variable = str(lst[2])
            if variable not in variables:
                print("ERROR: Use of Undefined Variable")
            else: 
                opcode = mydict.get(lst[0])
                reg1 = registers.get(lst[1])
                for i in range(0, len(variables)):
                    if variables[i] == variable:
                        memaddr = str(bin(ct+i).replace("0b",""))
                        memaddr = (8 - len(memaddr))*"0" + str(memaddr)
                        strD = opcode + reg1 + memaddr
                        print(strD)
                    else:
                        pass
        else:   
            print("ERROR: Register not found")
    except:
        print('ERROR: Instruction not in ISA')          


def funcE(lst): 
    try:
        len(lst) == 2
        label = str(lst[1])
        if label in  labels.keys():
            strE = ''
            opcode = mydict.get(lst[0])
            unused = '000'
            memaddr = str(bin(labels.get(label)).replace("0b",""))
            memaddr = (8 - len(memaddr))*"0" + str(memaddr)
            try:
                label not in variables  
                strE = opcode + unused + memaddr
                print(strE)
            except ValueError :
                print("ERROR: Name already exists as a Variable")
                pass            
        else:
            print("ERROR: Undefined Label")
    except:
        print('ERROR: Instruction not in ISA')   


def funcF(lst):
    try:
        len(lst)==1
        if (len(lst))==1:
            strF = ''
            opcode = mydict.get(lst[0])
            unused = '00000000000'
            strF = opcode + unused
            print(strF)
        else:
            print("ERROR: Incorrect Use of hlt")
    except:
        print('ERROR: Instruction not in ISA')   


c=0

opc=[]

for line in f1:
    
    if line=='\n':
        pass
    else:
        lst=line.split()
    
        if lst[0] == 'var':
            if c == 0:
                variables.append(lst[1])
            else:
                print("ERROR: Variable not declared at the beginning")
                pass
        elif lst[0].replace(":","") in labels.keys() and len(lst)==1:
                pass

        else:
            if 'FLAGS' in lst:
                if len(lst) == 3 and lst[0] == 'mov' and lst[1] in registers.keys():
                    lst[0]=str(lst[0])+"2"
                    funcC(lst)
                else:
                    print("ERROR: Illegal use of FLAGS register")

            if lst[0]=="hlt" and c+1!=ct2:
                print("ERROR: Incorrect use of Termination Statement")
                c+=1
                continue 
            if  lst[0].replace(":","") in labels.keys() and len(lst)>1:
                opc=lst.copy()
                opc1=opc.pop(0)
                
            else:
                opc=lst.copy()
            if opc[0] == 'mov':
                if opc[2] not in registers:
                    opc[0] = str(opc[0]) + '1'
                else:                    
                    opc[0] =  str(opc[0]) + '2'
            else:
                pass
            if opc[0] in type.keys():
                instype = type.get(opc[0])
            
                if instype == 'A':
                    (funcA(opc))

                elif instype == 'B':
                    (funcB(opc))

                elif instype == 'C':
                    (funcC(opc))

                elif instype == 'D':
                    (funcD(opc))

                elif instype == 'E':
                    if opc[1] in labelrepeat:
                        print('ERROR: Label Declared more than once')
                    else:
                        (funcE(opc))

                elif instype == 'F':
                    (funcF(opc))
            else:
                print("ERROR: Typos in Instruction name")
            c+= 1
a=[]
for lines in f1:
    if lines!="\n":
        a=lines.split()
if a[0]!="hlt":
    print("ERROR: Incorrect Termination")
