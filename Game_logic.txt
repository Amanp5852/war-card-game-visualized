import random
suits = ('Hearts', 'Diamonds', 'Spades', 'Clubs')
ranks = ('Two', 'Three', 'Four', 'Five', 'Six', 'Seven', 'Eight', 'Nine', 'Ten', 'Jack', 'Queen', 'King', 'Ace') 

values = {'Two':2, 'Three':3, 'Four':4, 'Five':5, 'Six':6, 'Seven':7, 'Eight':8, 
            'Nine':9, 'Ten':10, 'Jack':11, 'Queen':12, 'King':13, 'Ace':14}


class Cards():

    def __init__(self,suit,rank):
        self.suit = suit
        self.rank = rank
        self.values = values[rank]

    def __str__(self):
        return self.rank + " of " + self.suit

class Deck():

    def __init__(self):
        self.all_cards = []

        for suit in suits:
            for rank in ranks:
                created_cards = Cards(suit,rank)
                self.all_cards.append(created_cards)
                
    def shuffle(self):
        return random.shuffle(self.all_cards)

    def deal_one(self):
        return self.all_cards.pop()

class Player():

    def __init__(self,name):
        self.name = name
        self.all_cards = []

    def remove_one(self):
        return self.all_cards.pop(0)

    def add_cards(self,new_cards):
        if type(new_cards) == type([]):
            return self.all_cards.extend(new_cards)
        else:
            return self.all_cards.append(new_cards)

    def __str__(self):
        return f"Player {self.name} has {len(self.all_cards)} Cards"

# Game Setup
Player_one = Player("One")
Player_two = Player("Two")

new_deck = Deck()
new_deck.shuffle()

for x in range(26):
    Player_one.add_cards(new_deck.deal_one())
    Player_two.add_cards(new_deck.deal_one())

game_on = True

round = 0
while game_on:

    round += 1
    print(f"Number of rounds are {round}")

    if  len(Player_one.all_cards) == 0:
        print("Player Two Won, as Player One has no cards")
        game_on = False
        break

    if  len(Player_two.all_cards) == 0:
        print("Player One Won, as Player Two has no cards")
        game_on = False
        break

    player_one_on_table = []
    player_one_on_table.append(Player_one.remove_one())
    
    player_two_on_table = []
    player_two_on_table.append(Player_two.remove_one())

    at_war = True

    while at_war:
        if player_one_on_table[-1].values > player_two_on_table[-1].values:
            Player_one.add_cards(player_one_on_table)
            Player_one.add_cards(player_two_on_table)

            at_war = False

        if player_one_on_table[-1].values < player_two_on_table[-1].values:
            Player_two.add_cards(player_one_on_table)
            Player_two.add_cards(player_two_on_table)

            at_war = False

        else:
            print("War")

            if len(Player_one.all_cards) == 5:
                print("Player_one unable to Compete, beacuse of less cards")
                print("Player Two Wins")
                game_on = False
                break

            elif len(Player_two.all_cards) == 5:
                print("Player_two unable to Compete, because of less cards")
                print("Player one Wins")
                game_on = False
                break

            else:
                for cards in range(5):
                    player_one_on_table.append(Player_one.remove_one())
                    player_two_on_table.append(Player_two.remove_one())
                    
                
                

            