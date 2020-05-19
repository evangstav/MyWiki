= Channel Charting Implementation Notes = 


1) Frequency and time give close results untill now
2) noticed that the top left corner has significantly different pulses than the others. Considering removing them. I should check fisrt how they look.


## Supervised Approach
1) Classification
Assign labels to the whole datasets based on their true positions on the map. We used kmeans but can also be done by simple dividing the map into same sized areas and assign a label to each one.
By training on this kind of dataset we achieved an accuracy rate of 79% using 8 labels.

