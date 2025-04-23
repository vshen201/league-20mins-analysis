# Are League Games Decided at 20 Minutes, Even in Pro Play?

In this analysis, I explore various aspects of League of Legends games at the professional level, particularly focusing on data collected at the 20-minute mark. League of Legends is (unfortunately)
an incredibly popular game, with the highest level of competition drawing in tens of thousands of viewers
around the world. With so many fans invested in outcomes of games, I wondered: "how feasible is it to predict the outcomes of games at the highest level?"

## **Data Cleaning Process**

Before diving into the analysis, I cleaned the data to ensure that results could be more reliable. The key steps involved in cleaning the data are outlined below:

1. **Complete Data Selection**:
   - I included only games with **complete data** in the analysis. Complete data's biggest advantage over partial data is that it includes lots of statistics and performance metrics for both teams AND individual players.
   
2. **Filtering for Games Above 20 Minutes**:
   - To avoid outliers and null values, I specifically **only kept games where the game length exceeded 20 minutes**. This was important because games shorter than 20 minutes will have missing data, and the amount of games at the highest level which end before 20 minutes are few and far between.

3. **Handling Missing Values**:
   - No imputation was needed because I filtered using the above critieria. Imputing data is particularily difficult for a dataset like this because the performance metrics are already dependent on so many factors, that trying to compute them would risk being very inaccurate.

Head of final cleaned dataframe:

| killsat20_blue_bot | killsat20_blue_jng | killsat20_blue_mid | killsat20_blue_sup | killsat20_blue_top | assistsat20_blue_bot | assistsat20_blue_jng | assistsat20_blue_mid | assistsat20_blue_sup | assistsat20_blue_top | deathsat20_blue_bot | deathsat20_blue_jng | deathsat20_blue_mid | deathsat20_blue_sup | deathsat20_blue_top | killsat20_red_bot | killsat20_red_jng | killsat20_red_mid | killsat20_red_sup | killsat20_red_top | assistsat20_red_bot | assistsat20_red_jng | assistsat20_red_mid | assistsat20_red_sup | assistsat20_red_top | deathsat20_red_bot | deathsat20_red_jng | deathsat20_red_mid | deathsat20_red_sup | deathsat20_red_top | golddiffat20_bot | golddiffat20_jng | golddiffat20_mid | golddiffat20_sup | golddiffat20_top | xpdiffat20_bot | xpdiffat20_jng | xpdiffat20_mid | xpdiffat20_sup | xpdiffat20_top | csdiffat20_bot | csdiffat20_jng | csdiffat20_mid | csdiffat20_sup | csdiffat20_top | gamelength |
|--------------------|--------------------|--------------------|--------------------|--------------------|-----------------------|-----------------------|-----------------------|-----------------------|-----------------------|----------------------|----------------------|----------------------|----------------------|----------------------|--------------------|--------------------|--------------------|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|----------------------|---------------------|---------------------|---------------------|---------------------|---------------------|-------------------|-------------------|-------------------|-------------------|-------------------|------------------|------------------|------------------|------------------|------------------|------------------|------------------|------------------|------------------|------------------|------------|
| 0 | 0 | 1 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 1 | 4 | 2 | 1 | 0 | 1 | 3 | 4 | 0 | 0 | 5 | 4 | 1 | 6 | 0 | 0 | 0 | 0 | 1 | 0 | -2460 | -943 | -647 | 1475 | 825 | -3714 | -942 | -290 | 3137 | 326 | -126 | 5 | 14 | 126 | 18 | 1760 |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1748 | -139 | -934 | 726 | -530 | 460 | 342 | -586 | 241 | 737 | 22 | -7 | -27 | -9 | -1 | 2523 |
| 1 | 0 | 0 | 0 | 1 | 0 | 1 | 1 | 1 | 0 | 4 | 1 | 5 | 3 | 1 | 3 | 3 | 5 | 0 | 3 | 4 | 8 | 4 | 12 | 2 | 1 | 0 | 0 | 1 | 0 | -723 | -59 | -2143 | -739 | -64 | -488 | 1653 | -1795 | -1370 | 507 | -9 | 67 | -14 | 2 | 8 | 2249 |
| 2 | 0 | 2 | 1 | 1 | 1 | 5 | 2 | 2 | 0 | 1 | 2 | 2 | 1 | 0 | 4 | 2 | 0 | 0 | 0 | 1 | 4 | 3 | 6 | 0 | 0 | 2 | 2 | 1 | 1 | -182 | -400 | 2302 | 87 | 1136 | 927 | 542 | 386 | -255 | 1038 | 18 | -5 | 20 | -2 | 36 | 1805 |
| 2 | 2 | 0 | 0 | 1 | 3 | 3 | 2 | 4 | 3 | 1 | 3 | 1 | 3 | 0 | 0 | 1 | 5 | 1 | 1 | 5 | 7 | 2 | 4 | 2 | 1 | 1 | 1 | 1 | 1 | -915 | -299 | 386 | 1874 | 1735 | -757 | -1120 | -574 | 2203 | 603 | -134 | -23 | 23 | 142 | 34 | 2075 |


### **Counterpick Winrates**

One of the previous main focuses of this analysis was counterpick winrate. I calculated the winrate of champions when picked after the opposing champion of the same role. This has strategic implications because different champions often have weaknesses (think Fire Water Grass like Pokemon, but noticeably more complicated). This is useful for identifying champions that tend to perform well when played against certain opponents.

Here is an interactive plot displaying the counterpick winrates of champions:

<iframe
 src="assets/counterpick_wr.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

In this plot, you can see that counterpicking can have a significant impact on chances of victory, depending on the champion used to counter.

To create this plot, I filtered for counterpicks, grouped by champions, then took the average of wins to get a win rate. The aggregate table used for this is shown below:

| Champion   |   Winrate (%) |
|:-----------|--------------:|
| Naafiri    |     85.71     |
| Ambessa    |     83.33     |
| Kayn       |     71.43     |
| Elise      |     66.67     |
| Vel'Koz    |     66.67     |

### **Pick Order by Role**

Another important factor in team composition is the order in which champions are picked for each role, because it determines which roles on a team have to expose themselves first.

The following interactive plot illustrates the pick order across different roles:

<iframe
 src="assets/pickorder.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

The median values give lots of insight into how teams generally approach drafting roles. There's a general trend towards picking the top laner later in the draft, while securing bot laner and jungler roles early. A basic interpretation of this could be that getting counterpicked in bot and jungle matchups is not as impactful as getting counterpicked in top, mid, or support.

