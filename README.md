# lo
ONP algorythm
from sys import stdin

stala = ['a', 'b', 'c', 'd', 'e']
zmienna = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'R', 'S', 'T', 'U', 'W', 'X',
           'Y', 'Z']
funkcja = ['f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n']
sym_predykatywny = ['p', 'r', 's', 't', 'u', 'w', 'x', 'y', 'z']
operator = ["NOT", "~", "¬", "AND", "&", "∧", "OR", "|", "∨", "IMPLIES", "→", "IFF", "↔", "XOR", "⊕", "FORALL", "∀",
            "EXISTS", "∃"]


lines = stdin.read().splitlines()  # every line is one element in an array

for i in range(len(lines)):
    infix = []  # tutaj bedzie tworzyc się cala formula rachunku predykatow
    a = lines[i].split(" ")  # a - list of variables in i-th line
    for e in range(len(a)):
        if a[e] in stala or a[e] in zmienna:
            infix.append(a[e])  # odloz na stos
        elif a[e] in operator:
            a = infix.pop()  # zdejmij a[e-1]
            b = infix.pop()  # zdejmij a[e-2]
            infix.append(b + a[e] + a)  # odloz a[e-2], a[e], a[e-1] najlepiej jako jeden element
        elif a[e][0] in funkcja or a[e][0] in sym_predykatywny:
            arg = []  # lista argumentow funkcji
            for f in range(int(a[e][2])):
                arg[f] = infix.pop()  # zdejmij a[e][2] zmiennych ze stosu
            infix.append(a[e] + '(' + arg + ')')  # odloz a[e][0] ( a[e][2] argumentow )
