# Feline-reticulocytes
---

# Feline?
**Feline** is a member of the family **Felidae**. The family consists of 37 cat species that among others include the cheetah, puma, jaguar, leopard, lion, lynx, tiger, and domestic cat. For a detailed description, click [here](https://en.wikipedia.org/wiki/Felidae)

# What are reticulocytes?
**Reticulocytes** are immature red blood cells having a granular or reticulated appearance when suitably stained. You may wonder why this matters at all. After all, these are just immature blood cells but the fact is that a reticulocyte percentage that is higher than "normal" can be a sign of anemia. Anemia is one of the most frequent hematological abnormalities found in cats.
If you want to dig in about the disease and its causes, you can visit this [page](http://vetbook.org/wiki/cat/index.php?title=Anaemia)

# How can deep learning help in this?
Detecting and counting reticulocytes is time consuming. Also, it's not very easy to differentiate between different types of reticulocytes. This whole process from blood test to the time taken for confirmation by the vets is the time wasted just for the confirmation of disease. When not treated on time, anameia can be dangerous. Hence we need something that can aid the doctors to quickly identify the disease at an early stage. 

With the rise of deep learning in computer vision, one thing that has heavily improved over time is object detection and localization. The big question is: Can these state of the art object detectors be of any use in this scenario? And the answer is yes!!

For training, I used [TF object detection API](https://github.com/tensorflow/models/tree/master/research/object_detection). Recently, MobileNetv2 came out, the next generation of mobile nets which does an awesome job on the speed and accuracy tradeoff.
If you haven't read [this](https://arxiv.org/abs/1801.04381), then I would suggest you give it a read first. Also, I am assuming that you how Single shot detectors work. Although in-depth knowledge of that isn't required but until unless you understand it, it's harder to debug the network in the conditions when it's not working. 

---

# Dataset
The Feline-reticulocytes dataset was obtained from [Kaggle](https://www.kaggle.com/tentotheminus9/feline-reticulocytes). You can download it and look at the dataset how it has been arranged. For example, this is a sample image from the dataset


And the corresponding labels for the objects present in this image are arranged in an xml which looks like this:

```
<annotation>
	<folder>images</folder>
	<filename>000045.jpg</filename>
	<path>/home/vini/Desktop/data_300x300/images/000045.jpg</path>
	<source>
		<database>Unknown</database>
	</source>
	<size>
		<width>300</width>
		<height>300</height>
		<depth>3</depth>
	</size>
	<segmented>0</segmented>
	<object>
		<name>aggregate reticulocyte</name>
		<pose>Unspecified</pose>
		<truncated>0</truncated>
		<difficult>0</difficult>
		<bndbox>
			<xmin>140</xmin>
			<ymin>115</ymin>
			<xmax>169</xmax>
			<ymax>143</ymax>
		</bndbox>
	</object>
	<object>
		<name>punctate reticulocyte</name>
		<pose>Unspecified</pose>
		<truncated>0</truncated>
		<difficult>0</difficult>
		<bndbox>
			<xmin>72</xmin>
			<ymin>155</ymin>
			<xmax>103</xmax>
			<ymax>187</ymax>
		</bndbox>
	</object>
	<object>
		<name>erythrocyte</name>
		<pose>Unspecified</pose>
		<truncated>0</truncated>
		<difficult>0</difficult>
		<bndbox>
			<xmin>184</xmin>
			<ymin>195</ymin>
			<xmax>213</xmax>
			<ymax>228</ymax>
		</bndbox>
	</object>
</annotation>

```

There are a total of three classes of reticulocytes that we have to identify:
* Aggregate reticulocyte
* Erythrocyte
* Punctate reticulocyte

There are 1086 images in total for training data. Each image can either have a single object(blood cell) or multiple objects.

---

# Dependencies
