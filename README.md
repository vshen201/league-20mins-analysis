# Are League Games Decided at 20 Minutes, Even in Pro Play?

In this analysis, I explore various aspects of League of Legends games, particularly focusing on data collected at the 20-minute mark. I investigate key trends and insights, such as champion performance, counterpicks, and pick order. This analysis can inform strategic decisions based on the team's composition and champions' matchups.

## **Data Cleaning Process**

Before diving into the analysis, I performed an important cleaning process to ensure that the results would be accurate and reliable. The key steps involved in cleaning the data are outlined below:

1. **Complete Data Selection**:
   - I included only games with **complete data** in the analysis. This means that I ensured all relevant features, such as champion names, roles, winrates, and other game statistics, were present for every game.
   
2. **Maximizing Coverage**:
   - I focused on games from leagues with the **most complete data** to maximize the coverage of my analysis. This ensured that the analysis was not skewed by incomplete or sparse data, particularly from leagues with missing or unreliable statistics.

3. **Filtering Games Above 20 Minutes**:
   - To avoid outliers and null values, I specifically **only kept games where the game length exceeded 20 minutes**. This was important because games shorter than 20 minutes often had incomplete data or outliers that could distort the results.

4. **Handling Missing Values**:
   - I did not perform any data imputation because I **ignored any rows with NaN values**. Instead of trying to fill in missing data (which could introduce inaccuracies), I excluded incomplete games from the dataset entirely. This approach ensured that only games with complete data were analyzed.

With the dataset cleaned and prepared, I proceeded to explore key trends and insights.

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
