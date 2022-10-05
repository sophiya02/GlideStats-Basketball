# Basketball-StatsNow
Basketball StatsNow is a ServiceNow application built using the balldontlie.io API open source project. balldontlie.io is a free API with no signup or key required.

<b>Features:</b>
-Translates all endpoints available on balldontlie.io to the ServiceNow platform
-Automated daily job grabs all game data and player statlines from the previous day, and updates season average records for all players who played. It will also update automatically update a player's current listed team if they are traded or change teams, and create new Player records for anyone making their NBA debut.
-Recommended setup script automatically grabs all current NBA teams, all NBA players since 1979, game data since the beginning of the 2020 season, and all player statlines for the previous month
-All calls have built in wait timers as to not exceed the balldontlie.io rate limit of 60 calls per minute.

<b>Installation Guide:</b> Coming soon

There is a script library called BasketballUtils that does most of the heavy lifting. You can leverage the functions here to pull in whatever NBA data you want; 1979 to present day. balldontlie.io API game stats are updated every ten minutes.

<b>BasketballUtils functions:</b>

<b>getTeams()</b> - Retrieves all current NBA teams and saves the data to the Teams table. Example usage: 
new BasketballUtils().getTeams();

<b>getAllPlayers()</b> - Retrieves all NBA players from 1979 to current day and saves the data to the Players table. Example usage:
new BasketballUtils().getAllPlayers();

<b>getPlayerByID(id)</b> - Retrieves information about a single player by ID and writes the data to the Players table; ID can be found on the Players table after running getAllPlayers(). This is typically only used to determine team changes. Example usage: 
new BasketballUtils().getPlayerByID('322');

<b>getGamesByDate(date)</b> - Retrieves information about all games played on a single date and writes the data to the Games table. Example usage:
new BasketballUtils().getGamesByDate('2022-04-28');

<b>getGamesByDateRange(date1, date2)</b> - Retrieves information about all games played during a date range and writes the data to the Games table. Example usage:
new BasketballUtils().getGamesByDateRange('2022-01-01', '2022-03-31');

<b>getGameByID(id)</b> - Retrieves information about a single player by ID and writes the data to the Games table; ID can be found on the Games table after running getGamesByDate() or getGamesByDateRange(). Example usage:
new BasketballUtils().getGameByID('22194');

<b>getPlayerStatsByGame(id)</b> - Retrieves all player statlines for a game and writes the data to the Player Game Stats table; Game ID can be found on the Games table after running getGamesByDate() or getGamesByDateRange(). Example usage:
new BasketballUtils().getPlayerStatsByGame('22194');

<b>getGameIDsByDate(date)</b> - Retrieves an array of all game IDs for games played on a specific date. Example usage:
var ids = new BasketballUtils().getGameIDsByDate('2022-04-28');

<b>getGameIDsByDateRange(date1, date2)</b> - Retrieves an array of all game IDs for games played during a range of dates. Example usage:
var ids = new BasketballUtils().getGameIDsByDateRange('2022-01-01', '2022-03-31');

<b>getYesterdayStatsForAllPlayers()</b> - Retrieves all player statlines from games the day before. If Game records have not yet been retrieved for the previous day, they will automatically be created. If any Player records do not exist for games played (NBA debut), they will automatically be created. Example usage:
new BasketballUtils().getYesterdayStatsForAllPlayers();

<b>getAllPlayerStatsByDate(date)</b> - Retrieves all player statlines for a specific date. If Game records have not yet been retrieved for that day, they will automatically be created. Example usage:
new BasketballUtils().getAllPlayerStatsByDate('2022-04-28');

<b>getAllSeasonAvgForPlayer(id)</b> - Retrieves season average records for every year for a single player, and saves the data to the Season Averages table; ID can be found on the Players table. Example usage:
new BasketballUtils().getAllSeasonAvgForPlayer('322');

<b>getSingleSeasonAvgForPlayer(season, id)</b> - Retrieves a season average record for a single year for a single player, and saves the data to the Season Averages table. Example usage:
new BasketballUtils().getSingleSeasonAvgForPlayer('322');

<b>getUpdatedSeasonAvgs()</b> - Retrieves updated season average record for all players who played yesterday, and saves the data to the Season Averages table. Example usage:
new BasketballUtils().getUpdatedSeasonAvgs();

<b>getGamesPlayersStatsByRange(date1, date2)</b> - Retrieves all games, players, and statlines for a range of dates. I recommend keeping your range to a month or less, as this call can take a while due to API limits. Example usage:
new BasketballUtils().getGamesPlayersStatsByRange('2022-01-01', '2022-01-31');

<b>getPlayerStatlinesByYear(id, year)</b> - Retrieves all single-game statlines for a player for an entire season, and saves them to the Player Game Stats table. Example usage:
new BasketballUtils().getPlayerStatlinesByYear('322', '2021);
