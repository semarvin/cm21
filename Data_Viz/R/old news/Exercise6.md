---
title: "Exercise 6"
output: html_document
---

Time: 5 hours

Following tutorial from the reading. Loading gapminder library and sample data.

```{r}
gapminder
```

```{r}
p <- ggplot(data = gapminder,
            mapping = aes(x= gdpPercap, y = lifeExp))
p + geom_point()
```

Success.

Chapter 3

```{r}
p <- ggplot(data = gapminder)
p <- ggplot(data = gapminder, mapping = aes(x=gdpPercap, y = lifeExp))
p
```

I learned that this does nothing. Needs geom_point(), I'm guessing. Back to reading.

```{r}
p + geom_point()
```

Confirmed.

```{r}
p + geom_smooth()
```

```{r}
p + geom_point() + geom_smooth()
```

A plot only a mother could love

```{r}
p + geom_point() + geom_smooth(method = "lm")
```

```{r}
p + geom_point() + geom_smooth(method = "gam") + scale_x_log10()
```

Very cool.

```{r}
p + geom_point() +
  geom_smooth(method = "gam") +
  scale_x_log10(labels = scales::dollar)
```

```{r}
p + geom_point() +
  geom_smooth(method = "gam") +
  scale_x_log10(labels = scales::comma)
```

```{r}
p <- ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp, color = "purple"))
p + geom_point() + geom_smooth(method = "loess") + scale_x_log10()
```

```{r}
p <- ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp))
p + geom_point(color = "purple") + geom_smooth(method = "loess") + scale_x_log10()
```

```{r}
p + geom_point(alpha = 0.3) + geom_smooth(color = "orange", se = FALSE, size = 8, method = "lm") + scale_x_log10()
```

My graph looks a little different than the one in the book. Instead of the whole layer of points being alpha = 0.3, each point is alpha = 0.3. I guess I can chalk this up to using ggplot2 instead of ggplot (since it's no longer supported in the version of R I'm using)?

```{r}
p + geom_point(alpha = 0.3) +
  geom_smooth(method = "gam") +
  scale_x_log10(labels = scales::dollar) +
  labs(x = "GDP Per Capita", y = "Life Expectancy in Years",
       title = "Economic Growth and Life Expectancy",
       subtitle = "Data points are country-years",
       caption = "Source: Gapminder.")
```

Ooh, fancy! I learned something new.

```{r}
p <- ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp, color = continent))
p + geom_point() + geom_smooth(method = "loess") + scale_x_log10()
```

love it

```{r}
p <- ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp, color = continent, fill = continent))
p + geom_point() + geom_smooth(method = "loess") + scale_x_log10()
```

I think that the other graph is easier to read? Maybe just me.

```{r}
p <- ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp))
p + geom_point(mapping = aes(color = continent)) +
  geom_smooth(method="loess") +
  scale_x_log10()
```

```{r}
p + geom_point(mapping = aes(color = log(pop))) + scale_x_log10()
```

```{r}
ggsave(filename = "my_figure.png")
```

Now starting to work on my own unfortunate visual I came up with a few weeks ago. Here's where I left off

```{r}
names <- read_csv("namestib.csv")
ggplot(data = names) +
 geom_point(mapping = aes(x = Role, y = Name, color = Source))
```

```{r}
p <- ggplot(data = names)
ggplot(data = names) + geom_point(mapping = aes(x = Source, y = Name))
```


```{r}
roles <- read_csv("rolestib.csv")
```

```{r}
ggplot(data = roles) + geom_point(mapping = aes(x = Role, y = Name, size = Count))
```

I like the idea of size = count (which is why I made this new tib) but I still don't like this graph. Except for the surrealists, not much is being communicated.

```{r}
ggplot(data = roles) + geom_point(mapping = aes(x = Count, y = Name, color = Role))
```

The color brightens the whole thing up, but makes the graph harder to read. What I'm trying to communicate is that the people mentioned the most were the surrealists, but I don't want to eliminate the other people/roles because I think they're important.

```{r}
ggplot(data = roles) + geom_point(mapping = aes(x = Name, y = Role, size = Count))
```

I really need to reevaluate what I want out of this visualization. I've hit a wall and nothing I'm doing looks quite right. I'm going back to the original table I was working with.

```{r}
names <- read_csv("namestib.csv")
ntib <- as_tibble(names)
ntib
```

```{r}
ggplot(data = ntib) + geom_point(mapping = aes(x = Name, y = Role))
```

Original table needs counts.

```{r}
nrc <- read_csv("nrc.csv")
```

```{r}
ggplot(data = nrc) + geom_point(mapping = aes(x = Name, y = Role, color = Count))
```

I really like this one, but there are two major issues here. 1: Using a gradient color scheme is not at all helpful in conveying the importance of the Count variable. 2: The names are all squished together and I don't want to make a massive chart, nor do I want to lose any data. Using only the names that were repeated proved to create very boring graphs. Tackling the issue no. 1 first:

```{r}
nrc <- read_csv("nrc.csv")
ggplot(data = nrc) + geom_point(mapping = aes(x = Name, y = Role, color = Count)) + scale_color_viridis(discrete = FALSE, option = "D", direction = -1)
```

This seems fine, though I'm also interested in exploring the RColorBrewer package.

```{r}
ggplot(data = nrc) + geom_point(mapping = aes(x = Name, y = Role, color = Count)) + scale_color_brewer(discrete = FALSE, palette = "Set1")
```

Well, no luck there. Maybe wesanderson will be fun.

```{r}
ggplot(data = nrc) + geom_point(mapping = aes(x = Name, y = Role, color = Count)) + scale_color_manual(values = wes_palette(n = 5, name = "Moonrise3", type = "discrete"))
```

Going backwards because I am new to this.
```{r}
names(wes_palettes)
```

Well, I could not figure that out either and it was a big waste of time. I'm a bit sick of this scatterplot and I've been trying to wrap my head around it for nearly a week now. I'm going to call it a day. This is just the best I can do with the data I have.

Adding labels:

```{r}
ggplot(data = nrc) + geom_point(mapping = aes(x = Name, y = Role, color = Count)) + scale_color_viridis(discrete = FALSE, option = "D", direction = -1) +
  labs(x = "Named Entities in Corpus S", y = "Roles of Entities",
       title = "Who were the Surrealists writing about?")
```

Just seeing one last time if size isn't a better variable to show count:

```{r}
ggplot(data = nrc) + geom_point(mapping = aes(x = Name, y = Role, size = Count, color = Count)) + scale_color_viridis(discrete = FALSE, option = "D", direction = -1) +
  labs(x = "Named Entities in Corpus S", y = "Roles of Entities",
       title = "Who were the Surrealists writing about?")
```


Okay, good enough. I'm not a big fan of the viridis palette aesthetically, but it'll do. I actually think combining it with size is more impactful, and leaving the size without color ends up hiding a lot of the smaller Surrealist points.


```{r}
ggsave(filename = "named_entities.png", width = 15)
```

Okay, 7 x 7 is not big enough to encompass all the names. Neither is 15 x 7. I'm so sick of scatterplots D: I know that a bar plot would be better but I feel like the assignment was a scatterplot.

Back to the drawing board. Working with a smaller and less interesting table:

```{r}
roles <- read_csv("rolestib.csv")
ggplot(data = roles) + geom_point(mapping = aes(x = Name, y = Role, size = Count, color = Count)) +  scale_color_viridis(discrete = FALSE, option = "D", direction = -1) + labs(x = "Named Entities in Corpus S", y = "Roles of Entities",
       title = "Who were the Surrealists writing about?")
```

```{r}
ggsave(filename = "named_entities_small.png", width = 15)
```

None of this is working!! So I'm going to hide the x axis values on the original desired chart. I wish that I could simply rotate them to read vertical.
WAIT

```{r}
ggplot(data = nrc) + geom_point(mapping = aes(x = Role, y = Name, size = Count, color = Count)) + scale_color_viridis(discrete = FALSE, option = "D", direction = -1) + labs(x = "Types of Entities", y = "Named Entities in Corpus S",
       title = "Who were the Surrealists writing about?")
```

```{r}
ggsave(filename = "named_entities.png", width = 27, height = 21)
```

I don't think it's humanly possible for me to hate this graph any more than I do at this moment right now.

It's done I hate it I also hate R markdown I am having quite a time with this horrid thing today

I then spent another 30 minutes trying to convert the stupid markdown file that I so loathe into a stupid HTML file so other humans can actually read it on GitHub but I am so frustrated and I love my little R Notebooks and wish I'd never ventured out into the horrible world of markdown