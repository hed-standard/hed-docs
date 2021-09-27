# 2. Getting started

Good annotation starts with understanding how your experiment unfolds during a session.

1. Do all of your event files have the same columns?  What are these columns and what do they represent?
2. What are the event values in the various columns? What do these values represent?
3. How are these events encoded?
4. What is the relationship of the events on the time line?

Experiment examples:
1. Simple oddball
2. Sternberg working memory
3. Wakeman-Hansen face recognition
4. Attention-shift data

The first step is: 


## 1.3. HED design principles

The near decade-long effort to develop effective event annotation for neurophysiological and behavioral data,
culminating to date in HED-3G, has revealed the importance of four principles (aka the PASS principles), 
all of which have roots in other fields:

````{admonition} **The PASS principles for HED design.**
:class: tip

1. **Preserve orthogonality** of concepts in specifying vocabularies.
2. **Abstract functionality** into layers (e.g., more general vs. more specific).
3. **Separate content** from presentation.
4. **Separate implementation** from the interface (for flexibility).
````

Orthogonality, the notion of keeping independently applicable concepts in separate hierarchies (1 above), 
has long been recognized as a fundamental principle in reusable software design, distilled in the design 
rule: *Favor composition over inheritance* (Gamma et al. 1994). 

Abstraction of functionality into layers (2) and separation of content from presentation (3) are well-known
principles in user-interface and graphics design that allow tools to maintain a single internal 
representation of needed information while emphasizing different aspects of the information when presenting 
it to users. 

Similarly, making validation and analysis code independent of the HEDschema (4) allows redesign of the 
schema without having to re-implement the annotation tools. A well-specified and stable API 
(application program interface) empowers tool developers.
