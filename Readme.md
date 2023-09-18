for i in range(101):
    if i % 10 == 0 and i != 0:
        if i == 10:
            print("Ten")
        elif i == 20:
            print("Twenty")
        elif i == 30:
            print("Thirty")
        elif i == 40:
            print("Forty")
        elif i == 50:
            print("Fifty")
        elif i == 60:
            print("Sixty")
        elif i == 70:
            print("Seventy")
        elif i == 80:
            print("Eighty")
        elif i == 90:
            print("Ninety")
        else:
            print("One Hundred")
    else:
        print(i)
        
This script uses a for loop to iterate through numbers from 0 to 100. It checks if the number is a multiple of 10 (i.e., every tenth number) and converts it to a wordy version using conditional statements. Otherwise, it prints the number itself.

When you run this script, it will print the numbers from 0 to 100 with every tenth number in wordy form.
