# Autostereogram Image Classification 

  

<br>- Course: Flatiron Data Science </br> 

<br>- Pace: Self Paced </br> 

<br>- Instructor: Jeff Herman </br> 

<br>- Author: [Cody D. Freese](mailto:c_freese@ymail.com) </br> 

![stock_magichat_800x800](https://user-images.githubusercontent.com/63601020/132889346-34ed3deb-148c-449b-8193-ba9d1ecda0cc.jpg)
![stock_magichat_h_350x350](https://user-images.githubusercontent.com/63601020/132889350-c7df0898-48dd-4d61-a99e-a24b163a1360.png)


# Business-Understanding: 

- As the world of AI increases in its use in everyday life as we see with Tesla self driving cars, the ability for programs to understand reality through the lens of which we see it will become ever more paramount. Whether this be within our visible spectrum range or increased to the full electromagnetic spectrum, eventually we will need to 'teach' computers the ability to 'see'. This is a small branch of that greater goal.  

- A stereogram, you've likely seen these when you were at your local dentists office, a collage of what seems to be random colors and symbols in a beautiful elaborate pattern. What some people would call an optical illusion or 3D hologram. When once relaxes their eyes and shifts their focus on the image, the 3 dimensional aspects make themselves known. 

- This is the first experiment to see if a program can learn to 'see' the 3D image within stereograms that we humans can see. This, I would hope, would lead to a greater project of helping programs distinguish reality from fallacy. 

- The eventual goal of combining this with a segmentation and object detection models to better understand how a program can 'see' 

![6728@2x](https://user-images.githubusercontent.com/63601020/132889340-d034bb19-1a29-4db2-bb93-2fe1d5a98bf2.jpg)  

# Data-Understanding: 

- Autostereogram collection made from introductory level of web scraping, manual retrieval and personal creation through the program Stereogram Explorer

- Opposing class was the collection of hidden images in each autostereogram, proportional to the amount that image appeared in the autostereogram collection
  

# Data-Preparation: 

- After being scraped I separate what images I have collected into stereograms, the hidden images, and a collection of images from real life of those hidden features. 

- When collection is finished I sorted my images into their subsequent sets:  

- Training set with 70% of my images 

- Validation set with 15% of my images 

- Test set with 15% of my images 

- I rescale my images to a binary 

- After verifying the size of my images I augmented the training data set and prepared for modeling. 

![6](https://user-images.githubusercontent.com/63601020/132888260-16962636-2e02-4428-9dc3-45da92dc650c.png)
![4](https://user-images.githubusercontent.com/63601020/132888264-a086e5e4-23c1-49b6-aada-4892a1a0659e.png)
![5](https://user-images.githubusercontent.com/63601020/132888275-c3541e0c-b034-468c-976b-42daa3effa08.png)

  

# Modeling 

- While not beneficial directly to the modeling process I intiated the modeling process on:
- Multi-Layer Perceptron, while this type of network doesn't provide the depth a convolutional neural network, it is a nice baseline.
- Convolutional Neural Network, giving the model the ability to use augmentation to highlight any hidden features
- Pretrain DenseNet201, ImageNet database to alleviate any vanishing gradient, enhance feature propagation and feature reuse.
- Each model Fintuned with ModelCheckpoint, EarlyStopping, and ReduceLROnPlateau with 'val_loss' as monitor.

 
# Evaluation: 

| Metrics           | Loss   | Accuracy | Precision | Recall |
|-------------------|--------|----------|-----------|--------|
| MLP Original      | 92.07% | 73.33%   | 68.84%    | 89.70% |
| MLP Finetune      | 48.15% | 79.68%   | 74.88%    | 92.12% |
| CNN Original      | 21.19% | 94.60%   | 95.12%    | 94.55% |
| CNN Finetune      | 15.78% | 95.24%   | 94.12%    | 96.97% |
| Pretrain Original | 16.11% | 95.56%   | 98.09%    | 93.33% |
| Pretrain Finetune | 17.14% | 93.97%   | 90.56%    | 98.79% |

- MLP model struggled to identify the difference but definitively was understanding what autostereograms were not.
- CNN performed outstandingly with the finetuned CNN performing a slightly higher recall

![7](https://user-images.githubusercontent.com/63601020/132888194-51e14311-4d24-48bb-9d87-e5f5d50e4de2.png)
![8](https://user-images.githubusercontent.com/63601020/132888198-6e0922bf-5ff1-46f3-a9c8-04d80130ac4e.png)
![9](https://user-images.githubusercontent.com/63601020/132888204-e501e26d-aa01-4576-a6fa-c814d26dbbc5.png)
![10](https://user-images.githubusercontent.com/63601020/132888208-cb3caf4d-d5f8-4274-915e-05ea17eb83ec.png)

- While these models work well in a general classification of what is and is not an autostereogram the model itself is not learning about the specific hidden image within each autostreogram, but rather is only understanding the difference between what makes an autostreogram and what doesn't.
- Next steps are to generate models for Object Detection and Segmentation, the next step to differentiate between the autostereogram and the image underneath
