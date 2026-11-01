def naive(text, pattern):
    n = len(text)
    m = len(pattern)
    found = []

    for i in range(n - m + 1):
        if text[i:i + m] == pattern:
            found.append(i)

    return found


text = input("Enter text: ")
pattern = input("Enter pattern: ")

result = naive(text, pattern)

if len(result) > 0:
    print("Pattern found at index:", result)
else:
    print("Pattern not found")