---
title: "Importance of Data Visualization"
excerpt: "Basic data visualization"
collection: learning
date: 2019-10-10

---

Basic of data visualizations
======

- In the field of Machine Learning, data visualization is not just making fancy graphics for reports. It is used extensively in day-to-day work for all phases of a project.
- To start with, visual exploration of data is the first thing one tends to do when dealing with a new task.
- We do preliminary checks and analysis using graphics and tables to summarize the data and leave out the less important details.
- It is much more convenient for us, humans, to grasp the main points this way than by reading many lines of raw data. It is amazing how much insight can be gained from seemingly simple charts created with available visualization tools.
- Next, when we analyze the performance of a model or report results, we also often use charts and images.
- Sometimes, for interpreting a complex model, we need to project high-dimensional spaces onto more visually intelligible 2D or 3D figures.
- All in all, visualization is a relatively fast way to learn something new about your data.
Thus, it is vital to learn its most useful techniques and make them part of your everyday ML toolbox.


Univariate visualization
-----
- Univariate analysis looks at one feature at a time.
- When we analyze a feature independently, we are usually mostly interested in the distribution of its values and ignore other features in the dataset.
- Below, we will consider different statistical types of features and the corresponding tools for their individual visual analysis.

    - **1.1 Quantitative features**
        - Quantitative features take on ordered numerical values.
        - Those values can be discrete, like integers, or continuous, like real numbers, and usually express a count or a measurement.

    - **Histograms and density plots**
        - The easiest way to take a look at the distribution of a numerical variable is to plot its histogram using the DataFrame's method hist().
        - A histogram groups values into bins of equal value range.
        - The shape of the histogram may contain clues about the underlying distribution type: Gaussian, exponential, etc.
        - You can also spot any skewness in its shape when the distribution is nearly regular but has some anomalies.
        - Knowing the distribution of the feature values becomes important when you use Machine Learning methods that assume a particular type (most often Gaussian).
        - There is also another, often clearer, way to grasp the distribution: density plots or, more formally, Kernel Density Plots.
        - They can be considered a smoothed version of the histogram.
        - Their main advantage over the latter is that they do not depend on the size of the bins.
        - It is also possible to plot a distribution of observations with seaborn's distplot().
        - By default, the plot displays the histogram with the kernel density estimate (KDE) on top.
        - The height of the histogram bars here is normed and shows the density rather than the number of examples in each bin.

    - **Box plot**
        - Another useful type of visualization is a box plot. seaborn does a great job here
        - Let's see how to interpret a box plot.
        - Its components are a box (obviously, this is why it is called a box plot), the so-called whiskers, and a number of individual points (outliers).
        - The box by itself illustrates the interquartile spread of the distribution, its length is determined by the  25th(Q1)  and  75th(Q3)  percentiles.
        - The vertical line inside the box marks the median ( 50% ) of the distribution.
        - The whiskers are the lines extending from the box.
        - They represent the entire scatter of data points, specifically the points that fall within the interval  (Q1−1.5⋅IQR,Q3+1.5⋅IQR) , where  IQR=Q3−Q1  is the interquartile range.
        - Outliers that fall outside of the range bounded by the whiskers are plotted individually as black points along the central axis.

    - **Violin plot**
        - The last type of distribution plots that we will consider is a violin plot.
        - The difference between the box and violin plots is that the former illustrates certain statistics concerning individual examples in a dataset while the violin plot concentrates more on the smoothed distribution as a whole.

    - **1.2 Categorical and binary features**
        - Categorical features take on a fixed number of values.
        - Each of these values assigns an observation to a corresponding group, known as a category, which reflects some qualitative property of the example.
        - Binary variables are an important special case of categorical variables when the number of possible values is exactly 2.
        - If the values of a categorical variable are ordered, it is called ordinal.

    - **Frequency table**
        - First, we will get a frequency table, which shows how frequent each value of the categorical variable is.
        - For this, we will use the value_counts() method.
        - By default, the entries in the output are sorted from the most to the least frequently-occurring values.
        - In case, the data is not balanced. i.e our two target classes, e.g loyal and disloyal customers, fraud or not fraud,etc are not represented equally in the dataset. Only a small part of the clients churned or are fraud.
        - This fact may imply some restrictions on measuring the classification performance, in the future, we may want to additionaly penalize our model errors in predicting the minority "Churn" class.

    - **Bar plot**
        - The bar plot is a graphical representation of the frequency table.
        - The easiest way to create it is to use the seaborn's function countplot().
        - There is another function in seaborn that is somewhat confusingly called barplot() and is mostly used for representation of some basic statistics of a numerical variable grouped by a categorical feature.

    - **Histograms Vs Bar plot**
        - Histograms are best suited for looking at the distribution of numerical variables while bar plots are used for categorical features.
        - The values on the X-axis in the histogram are numerical; a bar plot can have any type of values on the X-axis: numbers, strings, booleans.
        - The histogram's X-axis is a Cartesian coordinate axis along which values cannot be changed; the ordering of the bars is not predefined. Still, it is useful to note that the bars are often sorted by height, that is, the frequency of the values. Also, when we consider ordinal variables, the bars are usually ordered by variable value.

Multivariate visualization
-----
- Multivariate plots allow us to see relationships between two and more different variables, all in one figure.
- Just as in the case of univariate plots, the specific type of visualization will depend on the types of the variables being analyzed.

    - **2.1 Quantitative vs. Quantitative**

        - **Correlation matrix**
            - Let's look at the correlations among the numerical variables in our dataset.
            - This information is important to know as there are Machine Learning algorithms (for example, linear and logistic regression) that do not handle highly correlated input variables well.
            - First, we will use the method corr() on a DataFrame that calculates the correlation between each pair of features.
            - Then, we pass the resulting correlation matrix to heatmap() from seaborn, which renders a color-coded matrix for the provided values.

        - **Scatter plot**
            - The scatter plot displays values of two numerical variables as Cartesian coordinates in 2D space.
            - Scatter plots in 3D are also possible.
            - There is a slightly fancier option to create a scatter plot with the seaborn library
            - The function jointplot() plots two histograms that may be useful in some cases.
            - Using the same function, we can also get a smoothed version of our bivariate distribution
            - This is basically a bivariate version of the Kernel Density Plot discussed earlier.
    
        - **Scatterplot matrix**
            - In some cases, we may want to plot a scatterplot matrix.
            - Its diagonal contains the distributions of the corresponding variables, and the scatter plots for each pair of variables fill the rest of the matrix.

    - **2.2 Quantitative vs. Categorical**
        - In this section, we will make our simple quantitative plots a little more exciting.
        - We will try to gain new insights for target (dependent feature) prediction from the interactions between the numerical and categorical features.
        - More specifically, let's see how the input variables are related to the target variable.
        - Additionally, their points can be color or size coded so that the values of a third categorical variable are also presented in the same figure.
        - We can achieve this with the scatter() function but, let's try a new function called lmplot() and use the parameter hue to indicate our categorical feature of interest:

    - **2.3 Categorical vs. Categorical**
        - As we saw earlier in this article, if the variable has few unique values and, thus, can be considered either numerical or ordinal.
        - We have already seen its distribution with a count plot. Now, we are interested in the relationship between this ordinal feature and the target variable e.g Churn.
        - Let's look at the distribution of the number of calls to customer service, again using a count plot. This time, let's also pass the parameter hue=Churn that adds a categorical dimension to the plot

        - **Contingency table**
            - In addition to using graphical means for categorical analysis, there is a traditional tool from statistics: a contingency table, also called a cross tabulation.
            - It shows a multivariate frequency distribution of categorical variables in tabular form.
            - In particular, it allows us to see the distribution of one variable conditional on the other by looking along a column or row.

Whole dataset visualizations
-----
- **3.1 A naive approach**
    - We have been looking at different facets of our dataset by guessing interesting features and selecting a small number of them at a time for visualization.
    - We have only dealt with two to three variables at once and were easily able to observe the structure and relationships in data.
    - But, what if we want to display all the features and still be able to interpret the resulting visualization?
    - We could use hist() or create a scatterplot matrix with pairplot() for the whole dataset to look at all of our features simultaneously.
    - But, when the number of features is high enough, this kind of visual analysis quickly becomes slow and inefficient.
    - Besides, we would still be analyzing our variables in a pairwise fashion, not all at once.

- **3.2 Dimensionality reduction**
    - Most real-world datasets have many features, sometimes, many thousands of them.
    - Each of them can be considered as a dimension in the space of data points.
    - Consequently, more often than not, we deal with high-dimensional datasets, where entire visualization is quite hard.
    - To look at a dataset as a whole, we need to decrease the number of dimensions used in visualization without losing much information about the data.
    - This task is called dimensionality reduction and is an example of an unsupervised learning problem because we need to derive new, low-dimensional features from the data itself, without any supervised input.
    - One of the well-known dimensionality reduction methods is Principal Component Analysis (PCA), which we will study later in this course.
    - Its limitation is that it is a linear algorithm that implies certain restrictions on the data.
    - There are also many non-linear methods, collectively called Manifold Learning. One of the best-known of them is t-SNE.

- **3.3 t-SNE**
    - The name of the method looks complex and a bit intimidating: t-distributed Stohastic Neighbor Embedding.
    - Its math is also impressive (we will not delve into it here, but, if you feel brave, [here](http://www.jmlr.org/papers/volume9/vandermaaten08a/vandermaaten08a.pdf) is the original article by Laurens van der Maaten and Geoffrey Hinton from JMLR).
    - Its basic idea is simple: find a projection for a high-dimensional feature space onto a plane (or a 3D hyperplane, but it is almost always 2D) such that those points that were far apart in the initial n-dimensional space will end up far apart on the plane. Those that were originally close would remain close to each other.
    - Essentially, neighbor embedding is a search for a new and less-dimensional data representation that preserves neighborship of examples.
    - **Disadvantages of t-SNE:**
        - High computational complexity. The implementation in scikit-learn is unlikely to be feasible in a real task. If you have a large number of samples, you should try Multicore-TSNE instead.
        - The plot can change a great deal depending on the random seed, which complicates interpretation. In general, you shouldn’t make any far-reaching conclusions based on such graphs because it can equate to plain guessing. Of course, some findings in t-SNE pictures can inspire an idea and be confirmed through more thorough research down the line, but that does not happen very often.
        - Occasionally, using t-SNE, you can get a really good intuition for the data. The following is a good paper that shows an example of this for handwritten digits: Visualizing MNIST.
    - let's do some practice. First, we need to import some additional classes.
    - We need to discard non-numeric values and convert the values "Yes"/"No" of the binary features into numerical values using pandas.Series.map()
    - We also need to normalize the data. For this, we will subtract the mean from each variable and divide it by its standard deviation. All of this can be done with StandardScaler.
    - Then build a t-SNE representation and plot it.
    

        {% highlight ruby %}
            from sklearn.manifold import TSNE
            from sklearn.preprocessing import StandardScaler

            tsne_repr = tsne.fit_transform(X_scaled)

            plt.scatter(tsne_repr[:, 0], tsne_repr[:, 1], alpha=.5);
        {% endhighlight ruby %}