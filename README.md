# 18-03-2021
install.packages('tidyverse')
library('tidyverse')
kaggle <- read_csv("data/kaggle_survey_2018.csv", skip = 1)



iris %>%
  group_by(Species) %>%
  mutate(min_pl = min(Petal.Width),
         icecream = max(Petal.Width),
         mean_icecream = mean(Petal.Width)) %>% View()

iris %>%
  + group_by(Species) %>%
  + mutate(min_pl=min(Petal.Length),
           + icecream=max(Petal.Length),
           + mean_icecream=mean(Petal.Length)) %>% View()

> kaggle %>% 
  +     group_by(`What is your gender? - Selected Choice`) %>% 
  +     count()

kaggle %>% 
  +     group_by(`What is your gender? - Selected Choice`) %>% 
  +     count()
# A tibble: 4 x 2
# Groups:   What is your gender? - Selected Choice [4]
`What is your gender? - Selected Choice`     n
<chr>                                    <int>
  1 Female                                    4010
2 Male                                     19430
3 Prefer not to say                          340
4 Prefer to self-describe                     79
> 4010/ nrow(kaggle)
[1] 0.1680707


kaggle %>% 
  rename(gender = `What is your gender? - Selected Choice`) %>%
  filter(gender %in% c('Male','Female')) %>%
  group_by(gender) %>%
  count() %>%
  mutate(percentage = n / nrow(kaggle)) %>%
  ggplot() + geom_col(aes(x = gender,
                          y = percentage))



kaggle %>% 
  rename(gender = `What is your gender? - Selected Choice`) %>%
  filter(gender %in% c('Male','Female')) %>%
  group_by(gender) %>%
  count() %>%
  mutate(percentage = n / nrow(kaggle)) %>%
  ggplot() + geom_col(aes(x = gender,
                          y = n, fill = gender)) +
  geom_label(aes(x = gender,
                 y = n, label = n)) +
  #scale_y_log10() +
  labs(title = 'Kaggle Survey 2018 - Gender Count',
       x = 'Gender',
       y = 'Count') 
