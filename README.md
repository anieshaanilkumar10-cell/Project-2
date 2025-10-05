# Project-2
#include <stdio.h>
#include <string.h>

#define MAX 100

typedef struct {
    char data[MAX];
    int top;
} Stack;

void initStack(Stack *s) {
    s->top = -1;
}

void push(Stack *s, char c) {
    if (s->top < MAX - 1) {
        s->data[++(s->top)] = c;
    }
}

char pop(Stack *s) {
    if (s->top != -1) {
        return s->data[(s->top)--];
    }
    return '\0';
}

int isEmpty(Stack *s) {
    return s->top == -1;
}

int isValidParentheses(char *str) {
    Stack s;
    initStack(&s);

    for (int i = 0; str[i]; i++) {
        switch (str[i]) {
            case '(':
            case '[':
            case '{':
                push(&s, str[i]);
                break;
            case ')':
                if (isEmpty(&s) || pop(&s) != '(') return 0;
                break;
            case ']':
                if (isEmpty(&s) || pop(&s) != '[') return 0;
                break;
            case '}':
                if (isEmpty(&s) || pop(&s) != '{') return 0;
                break;
        }
    }

    return isEmpty(&s);
}

int main() {
    char str[MAX];
    printf("Enter a string: ");
    fgets(str, sizeof(str), stdin);
    str[strcspn(str, "\n")] = 0;

    if (isValidParentheses(str)) {
        printf("The parentheses are balanced.\n");
    } else {
        printf("The parentheses are not balanced.\n");
    }

    return 0;
}
