# Brisbane 2032 Olympics — Sports Fan Support Strategy
### Australian Sports Commission (ASC) Data Analytics Project
**QUT IFN619 — Data Analytics for Strategic Decision Makers**

---

## 📋 Project Overview

This project was conducted as a Data Scientist assisting the Australian Sports Commission (ASC) in building fan support for the Brisbane 2032 Olympic Games. The strategy focuses on connecting with school-age children and youth (aged 5-17) to develop a long-term fan base for Olympic athletes.

The analysis spans two assignments covering structured and unstructured data analytics across five analytical cycles.

---

## 🎯 Scenario

The ASC needs to build fan support for athletes over the next 6 years through strategically connecting with school-age children and youth because:
- Children participating in sports now are likely peers of future 2032 Olympians
- High participation sports have natural fan-athlete connection potential
- Early adolescents will become young adults by 2032 — prime social media advocates
- Australia's social media ban for under-16s creates an opportunity to attract youth to sports

## 📊 Assignment 1 — Foundational Data Analytics

### Cycle 1: Structured Analysis — AusPlay Participation Data

**Question:** Which top 10 confirmed Brisbane 2032 Olympic sports have the highest estimated number of participants among children and youth aged 5-17 in Australia?

**Data:** AusPlay By Sport Data Tables (July 2024 — June 2025)
- Sheet 2: Children participation (ages 5-14)
- Sheet 1: Adults participation (15-17 age group only)
- Combined and filtered to 27 confirmed Brisbane 2032 Olympic sports

**Key Data Decisions:**
- Excluded 0-4 age group — too young for meaningful fan engagement
- Combined Shooting/field and Shooting/range into single Shooting category
- Removed `**` flagged data (>100% margin of error)
- Cross-referenced with confirmed Brisbane 2032 Olympic sports list

**Analysis & Key Findings:**

<img width="1200" height="700" alt="Bar chart — Top 10 Most Participated Olympic Sports (Ages 5-17)" src="https://github.com/user-attachments/assets/c0e5094f-1534-4075-9b0b-5e6e2b115bfc" />

Top 10 most participated confirmed Brisbane 2032 Olympic sports:
1. Swimming — 1.32M participants
2. Football/soccer — 882K participants
3. Basketball — 502K participants
4. Gymnastics — 364K participants
5. Tennis — 281K participants
6. Athletics, track and field — 205K participants
7. Cycling — 142K participants
8. Volleyball — 131K participants
9. Badminton — 110K participants
10. Table tennis — 73K participants

Swimming and Football/soccer combined account for more than half of total participation across all top 10 sports.

<img width="1200" height="700" alt="Faceted bar chart — Age Group Distribution within Top 10 Sports" src="https://github.com/user-attachments/assets/4225481f-4198-40ce-b8c1-c488aeac4863" />


**Age Group Trend Categories (Manual Classification):**
- **U-shaped trend:** Swimming, Football/soccer — peak at young ages, dip at 12-14, recover at 15-17
- **Increasing with age:** Basketball, Volleyball, Badminton, Table tennis
- **Decreasing with age:** Gymnastics
- **Relatively stable:** Athletics, Tennis, Cycling

**Strategic Recommendations:**
- ASC should prioritise Swimming and Football/soccer — largest natural fan bases
- For increasing sports — target 12-17 age group for fan engagement
- For decreasing sports — target 5-8 age group urgently before drop-off
- For stable sports — consistent investment across all age groups

---

### Cycle 2: Semi-Structured Analysis — Guardian API (Social Media Ban)

**Question:** What are the key themes in Guardian Australia's coverage of the Australian social media ban for under-16s?

**Data:** Guardian API
- Search: `"social media" AND "age ban" AND Australia`
- Production office: aus
- Date range: September 2024 — April 2026
- 49 articles fetched → filtered to 15 relevant articles

**Analysis:** CountVectorizer word frequency analysis
- max_df=0.86, min_df=2, max_features=500, stop_words="english"

<img width="1000" height="800" alt="Horizontal bar chart — Top 30 Most Frequent Words" src="https://github.com/user-attachments/assets/20586073-45a2-44a3-b357-eeaec32c08e5" />


**Key Themes Identified (Manual Clustering):**

| Theme | Words | Total Count |
|---|---|---|
| Political & Legislative | minister, albanese, legislation, parliament | 164 |
| Implementation & Enforcement | assurance, trial, technology, access, digital | 159 |
| People & Community | young, parents, guardian, 16 | 113 |
| Wellbeing & Harm | harm, mental, health, content | 63 |
| Social Media Platforms | instagram | 15 |

**Key Insight:** "young" dominated all word frequencies (58 occurrences) — media consistently framed the ban as a youth issue. Coverage focused on political debate rather than the underlying mental health concerns that drove the ban.

**Strategic Recommendations for ASC:**
- The 15-17 age group is the first eligible for social media — ASC should build digital fan engagement targeting this group
- By 2032, current 15-17 year olds will be 21-23 — prime financial supporters and digital advocates
- ASC should build a foundation for digital fan support now so younger groups can join when they turn 16

---

## 🤖 Assignment 2 — Applied Data Analytics

### Cycle 1: K-Means Clustering — Olympic Sports Participation Trends

**Question:** Can K-Means clustering confirm the participation trend categories identified in Assignment 1 and expand analysis to all 27 confirmed Brisbane 2032 Olympic sports?

**Data:** AusPlay By Sport Data Tables — df_olympic from Assignment 1
- Features: age group columns (5-8, 9-11, 12-14, 15-17)
- Row-wise normalisation using sklearn normalize(norm='l1')
- Removed Modern Pentathlon (zero participants) and Triathlon (unique pattern)
- 25 sports clustered

**Analysis:** K-Means clustering
- Tested k values 3-10 using loop
- Selected k=4 as optimal

<img width="900" height="500" alt="Line chart — Average Participation Trend by Cluster" src="https://github.com/user-attachments/assets/28bcee6d-edcc-47f5-8332-8bf9555ee909" />


**Cluster Results:**

| Cluster | Pattern | Sports |
|---|---|---|
| Cluster 0 | Stable/Mixed | Athletics, Basketball, Diving, Equestrian, Sailing, Football/soccer, Taekwondo, Tennis, Water polo |
| Cluster 1 | Strongly Increasing | Handball, Volleyball, Weight lifting, Table tennis, Wrestling, Canoeing, Badminton |
| Cluster 2 | Moderately Increasing | Fencing, Cycling, Boxing, Rowing, Shooting |
| Cluster 3 | Decreasing | Swimming, Gymnastics, Judo, Synchronised swimming |

**Comparison with Assignment 1:**
- K-Means confirmed three main patterns (stable, increasing, decreasing)
- The U-shaped category split — Football/soccer joined stable, Swimming joined decreasing
- K-Means revealed two distinct increasing patterns not identified manually

**Strategic Recommendations:**
- **Decreasing cluster:** Target 5-8 age group urgently — these children are most likely future Olympic athletes
- **Strongly Increasing:** Focus almost exclusively on 15-17 age group (70%+ of participation)
- **Moderately Increasing:** Target both 12-14 and 15-17 age groups
- **Stable/Mixed:** Consistent investment across all age groups

**Removed Sports Strategy:**
- Modern Pentathlon and Triathlon require a feeder sport approach — target children participating in individual disciplines (Swimming, Fencing, Cycling etc)

---

### Cycle 2: Barriers Analysis — What Stops Children from Playing Sport?

**Question:** What are the major barriers for children and youth aged 5-17 to participate in sports?

**Data:** AusPlay National Data Tables (January-December 2024)
- Table 14: Children barriers (ages 5-8, 9-11, 12-14)
- Table 13: Adult barriers (15-17 age group only)
- Removed barriers ASC cannot influence (disability, poor health, cultural factors)
- 11 actionable barriers retained

<img width="900" height="400" alt="1- separate bar charts — Top Barriers by Age Group (5-8, 9-11, 12-14, 15-17)" src="https://github.com/user-attachments/assets/7bd5a8b5-883e-4e7e-969f-59ff61c72da8" />

<img width="900" height="400" alt="2- separate bar charts — Top Barriers by Age Group (5-8, 9-11, 12-14, 15-17)" src="https://github.com/user-attachments/assets/9e9f4ce5-3695-42f7-8f83-89e4ece196af" />

<img width="900" height="400" alt="3- separate bar charts — Top Barriers by Age Group (5-8, 9-11, 12-14, 15-17)" src="https://github.com/user-attachments/assets/bf3822f6-6267-47e8-abaf-8e77fd4a4844" />

<img width="900" height="400" alt="4- separate bar charts — Top Barriers by Age Group (5-8, 9-11, 12-14, 15-17)" src="https://github.com/user-attachments/assets/fbf8afd1-eac9-42a8-942e-bc3145671bb8" />


**Key Findings:**

| Barrier | Pattern | Peak Age |
|---|---|---|
| `cant_afford` | Decreasing — highest overall (avg 14.4%) | 5-8 |
| `not_enough_time` | Strongly Increasing | 15-17 (16.9%) |
| `not_priority` | Fluctuating | 12-14 (12.2%) |
| `nobody_to_do_with` | Increasing | 15-17 (9%) |
| `no_transport` | Increasing | 15-17 (7.6%) |
| `no_longer_interested` | Peaks at 9-11 | 9-11 (7.7%) |

**Strategic Recommendations for ASC:**
1. **Financial support programs** — cost is the biggest overall barrier, especially for younger children
2. **Health and lifestyle awareness campaigns** — address not_priority and no_longer_interested
3. **Accessibility improvements** — better transport and more facilities
4. **Flexible scheduling** — critical for 15-17 age group

**Ethical Consideration:** Removing barriers ASC cannot influence means analysis focuses on more privileged segments of youth population. Children with disabilities, poor health or cultural barriers may be further disadvantaged.

---

### Cycle 3: LDA Topic Modelling — Social Media and Children's Mental Health

**Question:** What are the key themes in Guardian Australia's coverage of social media and children's mental health (2020-2024)?

**Data:** Guardian API
- Search: `"social media" AND "children" AND "mental health" AND Australia`
- Date range: January 2020 — September 2024 (post-COVID, pre-ban)
- 604 articles fetched → filtered to 20 relevant articles

**Analysis:** LDA Topic Modelling
- CountVectorizer: max_df=0.80, min_df=2, max_features=10,000
- Tested k=3 to k=10, selected k=7
- random_state=42 for reproducibility

<img width="734" height="635" alt="image" src="https://github.com/user-attachments/assets/4d951aa4-d4c3-48d6-9514-3995a860a53f" />


**Topics Identified:**

| Topic | Keywords | Interpretation |
|---|---|---|
| Topic 0 | age, parents, pandemic, use | Broad parental concern about children's social media use |
| Topic 1 | meta, news, publishers, facebook | Platform accountability and regulation |
| Topic 2 | — | Noise topic (very low weights) |
| Topic 3 | self, disorders, tiktok, videos | Self-diagnosis disorders on social media |
| Topic 4 | — | Noise topic (very low weights) |
| Topic 5 | mirror, platforms, content | Social media and self-image |
| Topic 6 | suicide, death, care, prevention | Youth suicide crisis |

**Key Findings:**
- 14 out of 20 articles fell under Topic 0 — media treated social media harm as one broad interconnected issue
- Topic 3 revealed children self-diagnosing mental disorders through TikTok — creating echo chambers
- Topic 6 revealed rising youth suicide rates linked to cyberbullying and online shame

**Connection to Assignment 1:**
Assignment 1 showed the political debate about the ban — Assignment 2 revealed the underlying mental health concerns that drove it.

**Strategic Recommendations:**
- ASC marketing campaign should target **both parents and children**
- Position sport as mental health solution — community, identity and purpose
- Sport protects against depression and suicide risk through team belonging and achievement
- Social media ban creates urgent window of opportunity — act now while children have free time

---

## 🔧 Tools & Technologies

- **Python** — pandas, plotly.express, sklearn, requests, json, re
- **Jupyter Notebook** — analysis and narrative
- **Guardian API** — unstructured text data
- **AusPlay Dataset** — structured participation data
- **Techniques:** K-Means Clustering, LDA Topic Modelling, Word Frequency Analysis, Data Cleaning, Data Visualisation

---

## 📚 Data Sources

- [AusPlay By Sport Data Tables](https://www.ausport.gov.au/clearinghouse/research/ausplay/results) — Australian Sports Commission
- [AusPlay National Data Tables](https://www.ausport.gov.au/clearinghouse/research/ausplay/results) — Australian Sports Commission
- [Guardian API](https://open-platform.theguardian.com/) — Guardian Australia articles
- [Brisbane 2032 Olympic Sports](https://www.timeout.com/australia/news/your-ultimate-guide-to-the-brisbane-olympics-2032-dates-sports-venues-and-more-072325) — Timeout Australia

---

## ⚠️ Ethical Considerations

- AusPlay data has margin of error flags (`*` and `**`) — conclusions about flagged sports treated with caution
- Removing uninfluenceable barriers may underrepresent disadvantaged youth groups
- Guardian Australia represents a single news outlet with specific political viewpoint
- Brisbane 2032 sports programme still being finalised — analysis uses confirmed core sports as baseline
- LDA is stochastic — random_state=42 ensures reproducibility

---

## 👤 Author

**Sepehr Amooeinejad**
QUT — IFN619 Data Analytics for Strategic Decision Makers
