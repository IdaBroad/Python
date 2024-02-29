import random

suits = ['♠', '♥', '♦', '♣']
ranks = ['2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K', 'A']
cards = [rank + suit for suit in suits for rank in ranks]

random.shuffle(cards)

player1_hand = cards[:17]
player2_hand = cards[17:34]
player3_hand = cards[34:51]
landlord_hand = cards[51:]

def play_card(hand, last_play=None):
    if last_play is None:
        return hand.pop()
    else:
        valid_cards = [card for card in hand if card > last_play]
        if valid_cards:
            return hand.pop(hand.index(max(valid_cards)))
        else:
            return None

print("Landlord's hand:", landlord_hand)
last_play = None
current_player = 1

while True:
    if current_player == 1:
        card = play_card(player1_hand, last_play)
        if card is None:
            current_player = 2
        else:
            last_play = card
            if not player1_hand:
                break
    elif current_player == 2:
        card = play_card(player2_hand, last_play)
        if card is None:
            current_player = 3
        else:
            last_play = card
            if not player2_hand:
                break
    else:
        card = play_card(player3_hand, last_play)
        if card is None:
            current_player = 1
        else:
            last_play = card
            if not player3_hand:
                break
