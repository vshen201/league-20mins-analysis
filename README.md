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


## **Counterpick Winrates**

One of the main focuses of this analysis is the counterpick winrate. I calculated the winrate of champions when they were selected to counter another champion in specific matchups. This is useful for identifying champions that tend to perform well when played against certain opponents.

Here is an interactive plot displaying the counterpick winrates of champions:

<iframe
 src="assets/counterpick_wr.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

From the plot, I observed which champions consistently have high winrates when selected as counterpicks against specific champions, providing insight into their effectiveness in those matchups.

## **Pick Order by Role**

Another important factor in team composition is the order in which champions are picked for each role. The pick order can impact the overall composition and balance of the teams. For instance, certain roles may prioritize certain champions over others depending on their effectiveness in the current meta or synergy with other champions.

The following interactive plot illustrates the pick order across different roles:

<iframe
 src="assets/pickorder.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>

By examining this plot, I gained an understanding of which champions are most commonly prioritized in each role, helping to inform strategies on champion selection during drafts.

## **Top 5 Champions by Winrate**

To further explore champion performance, I examined the top 5 champions with the highest winrates in the dataset. This can reveal which champions are currently performing well and may be valuable picks in future games.

Here is the table of the top 5 champions based on their winrate:

| Champion   |   Winrate (%) |
|:-----------|--------------:|
| Naafiri    |     85.71     |
| Ambessa    |     83.33     |
| Kayn       |     71.43     |
| Elise      |     66.67     |
| Vel'Koz    |     66.67     |

These champions have demonstrated consistent performance, winning a high percentage of their games, making them strong candidates for selection in future matchups.

## **Key Insights and Next Steps**

- **Counterpick Analysis**: Identifying champions with high winrates against specific counterpicks can help adjust strategies by focusing on counterpicks in the draft phase.
  
- **Pick Order Trends**: By understanding which champions are prioritized in the pick order for each role, I can make more informed decisions during champion selection. Prioritizing high-performing champions or those that synergize well with other picks can improve overall team composition.
  
- **Top Performing Champions**: The table of top-performing champions highlights some champions that are currently performing exceptionally well. Incorporating these champions into future team compositions may lead to better performance and outcomes.

## **Conclusion**

This analysis provides valuable insights into champion performance at the 20-minute mark, focusing on counterpicks, pick order, and winrate data. By utilizing this information, I can make more informed decisions during drafts, improving my chances of success in League of Legends. Future analyses can delve deeper into specific champion interactions, more granular match statistics, or explore different gameplay phases for a broader understanding of performance trends.

---

This analysis lays the foundation for improving team compositions and game strategies based on data-driven insights. The interactive plots and tables help visualize key trends and allow for better decision-making when selecting champions and strategizing for matchups.
