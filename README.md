# RPS Challenge

Task
-------

* Create a rock paper scissors game to play on the web
* Users should be able to register their names, pick an option of rock paper or scissors and then swap turns
* Players should be able to take turns at picking rock paper or scissors
* Game should address the following user stories:

### User Stories

```
As a marketeer
So that I can see my name in lights
I would like to register my name before playing an online game

As a marketeer
So that I can enjoy myself away from the daily grind
I would like to be able to play rock/paper/scissors
```
## To play the game

```
config.ru
```

### To run the tests

```
rspec
```

## Functionality

### Domain model

| Possible Objects            | Methods       |
| ----------------------------|:-------------:|
| Player 1                    | register_name |
| Player 2                    | pick_option   |
| Game                        | swap_turns    |
|                             | score         |

## Controller

We want to keep this as skinny as possible. Possible pages to include are:
```
# home page where the user enters their name

get ('/')
lets names get entered

  before do
    @game = Game.instance
  end

# method that posts names and creates the game instance
  post ('/play')
  @player_1 = Player.new(params[:name])
  @player_2 = Player.new(params[:name])
  @game = Game.create(player_1, player_2

# page with options for the current player to choose from
get('/play')
@current_player_name = @game.current_player.name

# method that works out the winner and redirects to other pages depending on the result
post('/result')
game.play(params[:choice])
if @game.game_over == true
  redirect /results
else
  redirect /play
end

# page with the winner revealed
get('/result')
@winner = game.winner

```

## Model

We want our model to do most of the heavy lifting behind the scenes while staying true to the DRY and SRP principles. The singleton principle would also help to ensure that we avoid pesky global variables.

```
class Game(player_1, player_2)

  def initialize
    @turn = true
    @results = Results.new
    player_1 = player_1
    player_2 = player_2
    @current_player =
    @winner = Results.winner
    end

# class methods for singleton principle

  def self.create(player_1, player_2)
    @game = Game.new(player_1, player_2)
  end

  def self.instance
    @game
  end

  def play(choice)
    @current_player.store_choice(choice)
    results.calculate_results
    game.over?
    switch_players
  end

  def turn?
    @true = !@true
  end

  def switch_players
    @true ? @current_player = player_1 : @current_player = player_2
    turn?
  end

  def game_over?
    if end_game == true

  end

  def end_game
    if results.winner = something
      return true
    else
    return false
    end
  end

end

# calculates who is the winner based on the options they chose

class Result < Game

attr_reader : winner

 def initialize(game.player_1, game.player_2)
 @player_1 = player_1
 @player_2 = player_2
 @winner
 end

 def calculate_result

 case choice

 when player_1.choice == player_2.choice
    winner = "It's a draw"
 when player_1.choice == "Rock" && player_2.choice == "Paper"
    winner = player_2
 when player_1.choice == "Scissors" && player_2.choice == "Rock"
    winner = player_2
 when player_1.choice == "Paper" && player_2.choice == "Scissors"
    winner = player_2
 else
  @winner = player_1
 end
end

# stores and fetches the players name and their selection

class Player(name)
  def initialize
    @name = name
    @choice = choice
  end
end
```

## Views

There will be 3 views in total. The controller will handle the exchange of data between each view and the model will facilitate how and when that data will be stored and evaluated in order to play the game.

View 1 -
erb :index
containting a form to input names

View 2 -
erb :play
name of the current player
containing a form and images for rock, paper Scissors

View 3 -
erb :results
the name of the winner
the name of both players and their choices
button to play again


## Bonus level 2: Rock, Paper, Scissors, Spock, Lizard

Use the _special_ rules ( _you can find them here http://en.wikipedia.org/wiki/Rock-paper-scissors-lizard-Spock_ )

## Basic Rules

- Rock beats Scissors
- Scissors beats Paper
- Paper beats Rock

In code review we'll be hoping to see:

* All tests passing
* High [Test coverage](https://github.com/makersacademy/course/blob/master/pills/test_coverage.md) (>95% is good)
* The code is elegant: every class has a clear responsibility, methods are short etc.
