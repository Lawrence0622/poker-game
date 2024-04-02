# poker-game
#check out the README file























































import random
import math
import matplotlib.pyplot as plt
player_rank = 0
tr = 0
sf = 0
foak = 0
fh = 0
f = 0
hsc = 0
win = 0
lose = 0
tie = 0
sf_list =[]
suit = None
while player_rank != 5000:
    poker =[]
    value = 1
    player_1 = []
    computer_1 = []
    for i in range(52):
        poker.append(value)
        value += 1
    print(poker)
    for i in range(1,11):
        card = random.choice(poker)
        if i%2 == 0:
            player_1.append(card)
        else:
            computer_1.append(card)
        poker.remove(card)
    player_1.sort()
    computer_1.sort()
    print(player_1)
    print(computer_1)
    print(poker)
    def trancard(input):
        true_input = []
        for i in input:
            number = math.ceil(i/4)
            if i%4 == 0:
                color =4
            else:
                color = i%4
            a = [color,number]
            true_input.append(a)
        
        return true_input
    #1-52的數字依序小到大為梅花、菱形、紅心和黑桃花色
    #5000-rank1,4000-rank2,3000-rank3,2000-rank4
    player_2 = trancard(player_1)
    computer_2 = trancard(computer_1)
    print(player_2)
    print(computer_2)
    def calculate(input_2):
        score = 0
        if input_2[0][0]==input_2[1][0]==input_2[2][0]==input_2[3][0]==input_2[4][0]:
            if input_2[0][1]+4 == input_2[1][1]+3 == input_2[2][1]+2 == input_2[3][1]+1 == input_2[4][1]:
                return 5000
            elif input_2[0][1] == 1 and input_2[1][1] == 10 and input_2[2][1] == 11 and input_2[3][1] == 12 and input_2[4][1] == 13:
                return 5000
            else:
                return 2000
        elif input_2[0][1] == input_2[1][1] == input_2[2][1] == input_2[3][1]:
            return 4000
        elif input_2[1][1] == input_2[2][1] == input_2[3][1] == input_2[4][1]:
            return 4000
        elif input_2[0][1] == input_2[1][1] and input_2[2][1] == input_2[3][1] == input_2[4][1]:
            return 3000
        elif input_2[0][1] == input_2[1][1] == input_2[2][1] and input_2[3][1] == input_2[4][1]:
            return 3000
        else:
            if input_2[0][1]+4 == input_2[1][1]+3 == input_2[2][1]+2 == input_2[3][1]+1 == input_2[4][1]:
                score = (input_2[0][1]+input_2[1][1]+input_2[2][1]+input_2[3][1]+input_2[4][1])*1.5
                return score
            elif input_2[0][1] == 1 and input_2[1][1] == 10 and input_2[2][1] == 11 and input_2[3][1] == 12 and input_2[4][1] == 13:
                score = (input_2[0][1]+input_2[1][1]+input_2[2][1]+input_2[3][1]+input_2[4][1])*1.5
                return score
            elif input_2[2][1] == input_2[3][1] == input_2[4][1]:
                score = (input_2[0][1]+input_2[1][1]+input_2[2][1]+input_2[3][1]+input_2[4][1])*1.3
                return score
            elif input_2[1][1] == input_2[2][1] == input_2[3][1]:
                score = (input_2[0][1]+input_2[1][1]+input_2[2][1]+input_2[3][1]+input_2[4][1])*1.3
                return score
            elif input_2[0][1] == input_2[1][1] == input_2[2][1]:
                score = (input_2[0][1]+input_2[1][1]+input_2[2][1]+input_2[3][1]+input_2[4][1])*1.3
                return score
            elif input_2[0][1] == input_2[1][1] or input_2[1][1] == input_2[2][1] or input_2[2][1] == input_2[3][1] or input_2[3][1] == input_2[4][1]:
                score = (input_2[0][1]+input_2[1][1]+input_2[2][1]+input_2[3][1]+input_2[4][1])*1.1
                return score
            else:
                score = (input_2[0][1]+input_2[1][1]+input_2[2][1]+input_2[3][1]+input_2[4][1])*1
                return score
    player_rank = calculate(player_2)
    computer_rank = calculate(computer_2)
    tr += 1
    if player_rank == 5000:
        sf += 1
    elif player_rank == 4000:
        foak += 1
    elif player_rank == 3000:
        fh += 1
    elif player_rank == 2000:
        f += 1
    else:
        hsc += 1
    if player_rank > computer_rank:
        win += 1
    elif player_rank < computer_rank:
        lose += 1
    else:
        tie += 1
    if player_rank == 5000:
        for i in range(5):
            sf_list.append(player_2[i][1])
        if player_2[0][0] == 1:
            suit = 'Clubs'
        elif player_2[0][0] == 2:
            suit = 'Diammods'
        elif player_2[0][0] == 3:
            suit = 'Hearts'
        else:
            suit = 'Spades'
file_w = open('PokerGame.txt','w')
file_w.write('Total round:'+ str(tr)+'\n')
file_w.write('Straight flush:'+str(sf)+'\n')
file_w.write('Four of a Kind:'+str(foak)+'\n')
file_w.write('Full house:'+str(fh)+'\n')
file_w.write('Flush:'+str(f)+'\n')
file_w.write('High Sum Card:'+str(hsc)+'\n')
file_w.write('=============================\n')
file_w.write('The straight flush you got:\n')
file_w.write('Suit='+suit+'\n')
file_w.write('Numbers='+str(sf_list)+'\n')
file_w.close()
wlt = [win,lose,tie]
slice_labels = ['Win','Lose','Tie']
plt.pie(wlt,labels = slice_labels,colors = ('#4682B4','#FFA500','g'),autopct = '%.2f%%')
plt.title('competition results')
plt.show()
print('Congradulation! You got straight flush!')
print('Pie plot finished!')
print('Data were written to PokerGame.txt')
