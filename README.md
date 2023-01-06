def main():
  # example budget
  budget = 1000000
  
  # example number of players to buy
  players = 2
  
  # suppose we have the data in a text file with the player stats where first column is the player name, 
  # and the last column is their real market price (based on recent transfer), and the columns in between are player statistics 
  # like pass% shot% minutes played, etc, and the player market value in last column
  train_data = np.genfromtxt(StringIO(train_string), skip_header=1)
    
  # split the data into coefficients (x) and market value (y) 
  player_train_value = train_data[:, -1]
  player_train_coefficents = train_data[:, 1:-1]
  
  # fit a linear regression model to the data and get the coefficients
  c = np.linalg.lstsq(player_train_coefficents, player_train_value)[0]

  # Test data has similar data format compared to train data
  player_data = np.genfromtxt(StringIO(test_string), skip_header=1)
  player_values = player_data[:, -1]
  player_coef_data = player_data[:, 1:-1]
  player_names = player_data[:, 0]
  
  # save the player data and print out the predicted market values for the players in the data set
  player_predicted_values = (player_coef_data @ c)
  print(player_predicted_values)
  
  # optimize the budget and players to buy
  # first create a list of players by market value vs current market value 
  relative_market_value = []
  for i in range(len(player_predicted_values):
    current_player = { name: player_names[i], value_gain: player_values[i] - player_predicted_values[i] }
    relative_market_value.append(current_player)
  
  print(relative_market_value)
  
  # algorythm to maximize the budget and amount of players to be implemented below
    
main()
