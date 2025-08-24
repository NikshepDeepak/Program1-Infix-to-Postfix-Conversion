
def precedence(op):
    if op == '+' or op == '-':
        return 1
    elif op == '*' or op == '/':
        return 2
    return 0


def is_operand(ch):
    return ch.isalnum()


def infix_to_postfix(expression):
    stack = []  # stack to hold operators
    result = ""  # postfix result

    for ch in expression:
        if is_operand(ch):
            result += ch
        elif ch == '(':
            stack.append(ch)
        elif ch == ')':
            while stack and stack[-1] != '(':
                result += stack.pop()
            stack.pop()  # remove '(' from stack
        else:
            while stack and precedence(stack[-1]) >= precedence(ch):
                result += stack.pop()
            stack.append(ch)

    # Pop remaining operators from stack
    while stack:
        result += stack.pop()

    return result


