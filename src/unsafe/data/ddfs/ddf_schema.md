Goal: create a single table to hold all damage functions in common format
    - store in parquet format (small file size, can be loaded directly as pandas df)
    - common format will preclude need for separate functions for handling ddfs.
        - can use parameters from single function to properly filter the ddf dataframe

Columns:

ddf_id: <!-- Suggest renaming to occtype to match NSI attribute -->
    dtype: object (string)
    description: Identifier for which type of structure the depth-damage value pertains to 
        (e.g. RES1-1SNB == Residential, single family, 1-story, no basement)

depth_ft:
    dtype: float64
    description: depth of flooding in feet in increments of 0.1ft.

ddf_source:
    dtype: object (string)
    description: Source of the damage function (e.g. Hazus, NACCS, USACE EGM, etc.)

params:
    dtype: object (list)
    description: parameters for the distribution of damage values
    <!-- 
        Suggest removing this column and replacing with dedicated columns for specific paremeter types.
            e.g. min, max, most_likely columns for NACCS ddfs; mean, st.dev for EGM ddfs
        And add a column to describe what distribution to sample from
    -->

dmg_dist:
    dtype: object (string)
    description: Type of statistical distribution to sample from for damage value (e.g, normal, triangular, uniform)

min:
    dtype: float64
    description: The minimum estimated damage value for the given depth and occtype

max:
    dtype: float64
    description: The maximum estimated damage value for the given depth and occtype

most_likely:
    dtype: float64
    description: The most likely estimated damage value for the given depth and occtype

mean:
    dtype: float64
    description: The mean estimated damage value for the given depth and occtype

sd:
    dtype: float64
    description: The standard deviation of the estimated damage value for the given depth and occtype