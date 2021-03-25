---
title: "Data Cleaning"
date: 2021-01-26T17:56:51-04:00
draft: false
---

All of the texts in Corpus AI and some of the texts in Corpus S were cleaned using regular expressions. Here's an example of my cleaning process:

Output from Tesseract:
```
accordion. The broom-seller’s heart froze with terror. The green sun and the
tears—also green—which extended as far as the eye could see, made it
perfectly clear what lilypad fate awaited him. He could not resign himself to
floating indefinitely on a sea of tears, even if it meant he would bloom with

large flowers.
Suddenly the sun yawned like a dog waking up, and breath reeking of

garlic polluted the atmosphere. A kazoo came and fell into the heap of

barbed wire the broom-seller was tangled in. He grabbed it and blew intoit.
A long whine and several tears emerged, which burst and expelled lumps of
foam all around, which floated on the sea of tears. Delighted, the broom-
seller continued to blow into the kazoo, continuing to to produce teary
fireworks which burst into foam and settled all about him. Of course, there
was the unfortunate whimpering of wounded beasts, but he got used to that.
This was a mistake, as they did not get used to him. When the sea of tears was
covered over with a thick rug of foam, circumstances changed rapidly for the
broom-seller, who had the unfortunate notion of lying down on it. Barely had
he stretched out when the kazoo’s whimpering became extraordinarily
loud. They were no longer whimpers but veritable roars which destroyed
his eardrums and slowly dug a tunnel through his head. When the tunnel was
completed, a train full of merchandise emerged from the barbed wire heap
and plunged into the tunnel from whence it never emerged. Meanwhile the
cattle-trucks gave way to platforms full of enormous machines whose
function no one could describe.

The broom-seller no longer had the strength to fight against his fate. He
was in shock, stupefied by the switchings, the collisions, the shuntings under
way in the tunnel in his head. Switching yard! Now he’d become a switching
yard! This thought was killing him and yet he continued to blow
mechanically into the kazoo, which let out more and more horrifying shrieks,
while the sun, overjoyed, burst out laughing and filled the air with a hideous
smell of garlic which the foam inhaled with delight. The foam puffed up
to the size of a tree-trunk. Suddenly the broom-seller expired like the
‘quack’ of a bugle and the trunks of foam clashed together in one immense
round of applause. But, although dead, the broom-seller was not yet a
corpse. This was obvious when he started to rub his hands, first gently
and then with a growing vigour, so much so that a high clear flame soon
spurted from between his palms which he squeezed and rubbed together
at a positively fantastic rate. When the flame had attained a height of a dozen
or so centimetres, the broom-seller was seized with convulsive somersaults,
and lava started to flow from his hands and then to fall into the tears, where

it produced huge jets of reddish steam which soon obscured the sun, even
though it was blowing upon it harder and harder. The garlic-saturated

atmosphere had become unbreathable, though it began to seem that the

114

```

Step 1: Select numbers to locate and erase page numbers and locate the common "I switched to 1" error. Use regex [0-9]

```
accordion. The broom-seller’s heart froze with terror. The green sun and the
tears—also green—which extended as far as the eye could see, made it
perfectly clear what lilypad fate awaited him. He could not resign himself to
floating indefinitely on a sea of tears, even if it meant he would bloom with

large flowers.
Suddenly the sun yawned like a dog waking up, and breath reeking of

garlic polluted the atmosphere. A kazoo came and fell into the heap of

barbed wire the broom-seller was tangled in. He grabbed it and blew intoit.
A long whine and several tears emerged, which burst and expelled lumps of
foam all around, which floated on the sea of tears. Delighted, the broom-
seller continued to blow into the kazoo, continuing to to produce teary
fireworks which burst into foam and settled all about him. Of course, there
was the unfortunate whimpering of wounded beasts, but he got used to that.
This was a mistake, as they did not get used to him. When the sea of tears was
covered over with a thick rug of foam, circumstances changed rapidly for the
broom-seller, who had the unfortunate notion of lying down on it. Barely had
he stretched out when the kazoo’s whimpering became extraordinarily
loud. They were no longer whimpers but veritable roars which destroyed
his eardrums and slowly dug a tunnel through his head. When the tunnel was
completed, a train full of merchandise emerged from the barbed wire heap
and plunged into the tunnel from whence it never emerged. Meanwhile the
cattle-trucks gave way to platforms full of enormous machines whose
function no one could describe.

The broom-seller no longer had the strength to fight against his fate. He
was in shock, stupefied by the switchings, the collisions, the shuntings under
way in the tunnel in his head. Switching yard! Now he’d become a switching
yard! This thought was killing him and yet he continued to blow
mechanically into the kazoo, which let out more and more horrifying shrieks,
while the sun, overjoyed, burst out laughing and filled the air with a hideous
smell of garlic which the foam inhaled with delight. The foam puffed up
to the size of a tree-trunk. Suddenly the broom-seller expired like the
‘quack’ of a bugle and the trunks of foam clashed together in one immense
round of applause. But, although dead, the broom-seller was not yet a
corpse. This was obvious when he started to rub his hands, first gently
and then with a growing vigour, so much so that a high clear flame soon
spurted from between his palms which he squeezed and rubbed together
at a positively fantastic rate. When the flame had attained a height of a dozen
or so centimetres, the broom-seller was seized with convulsive somersaults,
and lava started to flow from his hands and then to fall into the tears, where

it produced huge jets of reddish steam which soon obscured the sun, even
though it was blowing upon it harder and harder. The garlic-saturated

atmosphere had become unbreathable, though it began to seem that the
```

Step 2: Erase spacing to get everything on one line. Add spaces back in if necessary. Use regex \n

```
accordion. The broom-seller’s heart froze with terror. The green sun and the tears—also green—which extended as far as the eye could see, made it perfectly clear what lilypad fate awaited him. He could not resign himself to floating indefinitely on a sea of tears, even if it meant he would bloom with large flowers. 
Suddenly the sun yawned like a dog waking up, and breath reeking of garlic polluted the atmosphere. A kazoo came and fell into the heap of barbed wire the broom-seller was tangled in. He grabbed it and blew intoit. A long whine and several tears emerged, which burst and expelled lumps of foam all around, which floated on the sea of tears. Delighted, the broom- seller continued to blow into the kazoo, continuing to to produce teary fireworks which burst into foam and settled all about him. Of course, there was the unfortunate whimpering of wounded beasts, but he got used to that. This was a mistake, as they did not get used to him. When the sea of tears was covered over with a thick rug of foam, circumstances changed rapidly for the broom-seller, who had the unfortunate notion of lying down on it. Barely had he stretched out when the kazoo’s whimpering became extraordinarily loud. They were no longer whimpers but veritable roars which destroyed his eardrums and slowly dug a tunnel through his head. When the tunnel was completed, a train full of merchandise emerged from the barbed wire heap and plunged into the tunnel from whence it never emerged. Meanwhile the cattle-trucks gave way to platforms full of enormous machines whose function no one could describe. 
The broom-seller no longer had the strength to fight against his fate. He was in shock, stupefied by the switchings, the collisions, the shuntings under way in the tunnel in his head. Switching yard! Now he’d become a switching yard! This thought was killing him and yet he continued to blow mechanically into the kazoo, which let out more and more horrifying shrieks, while the sun, overjoyed, burst out laughing and filled the air with a hideous smell of garlic which the foam inhaled with delight. The foam puffed up to the size of a tree-trunk. Suddenly the broom-seller expired like the ‘quack’ of a bugle and the trunks of foam clashed together in one immense round of applause. But, although dead, the broom-seller was not yet a corpse. This was obvious when he started to rub his hands, first gently and then with a growing vigour, so much so that a high clear flame soon spurted from between his palms which he squeezed and rubbed together at a positively fantastic rate. When the flame had attained a height of a dozen or so centimetres, the broom-seller was seized with convulsive somersaults, and lava started to flow from his hands and then to fall into the tears, where it produced huge jets of reddish steam which soon obscured the sun, even though it was blowing upon it harder and harder. The garlic-saturated atmosphere had become unbreathable, though it began to seem that the
```

Step 3: Check for dashes to see if some words were separated by spacing which has now been removed. Use regex -

```
accordion. The broom-seller’s heart froze with terror. The green sun and the tears—also green—which extended as far as the eye could see, made it perfectly clear what lilypad fate awaited him. He could not resign himself to floating indefinitely on a sea of tears, even if it meant he would bloom with large flowers. 
Suddenly the sun yawned like a dog waking up, and breath reeking of garlic polluted the atmosphere. A kazoo came and fell into the heap of barbed wire the broom-seller was tangled in. He grabbed it and blew intoit. A long whine and several tears emerged, which burst and expelled lumps of foam all around, which floated on the sea of tears. Delighted, the broom-seller continued to blow into the kazoo, continuing to to produce teary fireworks which burst into foam and settled all about him. Of course, there was the unfortunate whimpering of wounded beasts, but he got used to that. This was a mistake, as they did not get used to him. When the sea of tears was covered over with a thick rug of foam, circumstances changed rapidly for the broom-seller, who had the unfortunate notion of lying down on it. Barely had he stretched out when the kazoo’s whimpering became extraordinarily loud. They were no longer whimpers but veritable roars which destroyed his eardrums and slowly dug a tunnel through his head. When the tunnel was completed, a train full of merchandise emerged from the barbed wire heap and plunged into the tunnel from whence it never emerged. Meanwhile the cattle-trucks gave way to platforms full of enormous machines whose function no one could describe. 
The broom-seller no longer had the strength to fight against his fate. He was in shock, stupefied by the switchings, the collisions, the shuntings under way in the tunnel in his head. Switching yard! Now he’d become a switching yard! This thought was killing him and yet he continued to blow mechanically into the kazoo, which let out more and more horrifying shrieks, while the sun, overjoyed, burst out laughing and filled the air with a hideous smell of garlic which the foam inhaled with delight. The foam puffed up to the size of a tree-trunk. Suddenly the broom-seller expired like the ‘quack’ of a bugle and the trunks of foam clashed together in one immense round of applause. But, although dead, the broom-seller was not yet a corpse. This was obvious when he started to rub his hands, first gently and then with a growing vigour, so much so that a high clear flame soon spurted from between his palms which he squeezed and rubbed together at a positively fantastic rate. When the flame had attained a height of a dozen or so centimetres, the broom-seller was seized with convulsive somersaults, and lava started to flow from his hands and then to fall into the tears, where it produced huge jets of reddish steam which soon obscured the sun, even though it was blowing upon it harder and harder. The garlic-saturated atmosphere had become unbreathable, though it began to seem that the
```

Step 4: Search for special characters and symbols to ensure that they belong there and clean up any remaining errors. Use regex \| and {}

```
accordion. The broom-seller’s heart froze with terror. The green sun and the tears—also green—which extended as far as the eye could see, made it perfectly clear what lilypad fate awaited him. He could not resign himself to floating indefinitely on a sea of tears, even if it meant he would bloom with large flowers. 
Suddenly the sun yawned like a dog waking up, and breath reeking of garlic polluted the atmosphere. A kazoo came and fell into the heap of barbed wire the broom-seller was tangled in. He grabbed it and blew intoit. A long whine and several tears emerged, which burst and expelled lumps of foam all around, which floated on the sea of tears. Delighted, the broom-seller continued to blow into the kazoo, continuing to to produce teary fireworks which burst into foam and settled all about him. Of course, there was the unfortunate whimpering of wounded beasts, but he got used to that. This was a mistake, as they did not get used to him. When the sea of tears was covered over with a thick rug of foam, circumstances changed rapidly for the broom-seller, who had the unfortunate notion of lying down on it. Barely had he stretched out when the kazoo’s whimpering became extraordinarily loud. They were no longer whimpers but veritable roars which destroyed his eardrums and slowly dug a tunnel through his head. When the tunnel was completed, a train full of merchandise emerged from the barbed wire heap and plunged into the tunnel from whence it never emerged. Meanwhile the cattle-trucks gave way to platforms full of enormous machines whose function no one could describe. 
The broom-seller no longer had the strength to fight against his fate. He was in shock, stupefied by the switchings, the collisions, the shuntings under way in the tunnel in his head. Switching yard! Now he’d become a switching yard! This thought was killing him and yet he continued to blow mechanically into the kazoo, which let out more and more horrifying shrieks, while the sun, overjoyed, burst out laughing and filled the air with a hideous smell of garlic which the foam inhaled with delight. The foam puffed up to the size of a tree-trunk. Suddenly the broom-seller expired like the ‘quack’ of a bugle and the trunks of foam clashed together in one immense round of applause. But, although dead, the broom-seller was not yet a corpse. This was obvious when he started to rub his hands, first gently and then with a growing vigour, so much so that a high clear flame soon spurted from between his palms which he squeezed and rubbed together at a positively fantastic rate. When the flame had attained a height of a dozen or so centimetres, the broom-seller was seized with convulsive somersaults, and lava started to flow from his hands and then to fall into the tears, where it produced huge jets of reddish steam which soon obscured the sun, even though it was blowing upon it harder and harder. The garlic-saturated atmosphere had become unbreathable, though it began to seem that the
```

Step 5: Ensure that text matches the original and is formatted correctly.

Clean up complete. This is highly representative of the process I use. This particular page only took a minute or two. Some texts/pages are more involved than others. On average, it probably takes me a few hours to parse through an entire text, especially since the surrealist texts I'm working with use creative and elaborte formatting which requires some hand-correction at times.