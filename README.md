
<div align="center">

<!-- TITLE -->
# VNHSGE: Vietnamese High School Graduation Examination Dataset for Large Language Models

</div>

VNHSGE is a dataset for large language models, collected from the Vietnamese National High School Graduation Examination and similar
exams.

> * Evaluates large language models in multitasks such as question answering, text generation, reading comprehension, visual question answering, and more.
> * Covers nine subjects including 300 essays on literature and 19,000 multiple-choice questions on other subjects including mathematics, physics, chemistry, biology, English, history, geography, and civic education
> * Contains both text and images
> * Vietnamese and English language supports

[![arXiv](https://img.shields.io/badge/cs.LG-arXiv:1234.56789-b31b1b.svg)](https://arxiv.org/abs/1234.56789)


VNHSGE dataset and other datasets:  the performance of ChatGPT and BingChat on the VNHSGE dataset is compared to other datasets in
the [GPT-4 Report](https://openai.com/research/gpt-4)


![alt text](https://github.com/Xdao85/VNHSGE/blob/main/Figures/VNHSGE_other_dataset.png?raw=true)

## Latest News
> * We will update evaluation set including 30 essay on literature and 1700 multiple choice questions one other subjects [5/30/2023].
> * Full dataset will be upload soon!

<!-- SETUP -->
## Dataset structure
VNHSGE dataset covers nice subjects including 300 essays on Literature and 19,000 multiple choice questions on other subjects. 

Subject | Type | Number of questions per exam | Number of exams | Question Total 
| :---: | :---: | :---: | :---: | :---:
Mathematics | Multiple choice | 50 | 50 | 2500
Literature | Essay | 6  | 50 | 300
English | Multiple choice | 50 | 50 | 2500
Physics | Multiple choice | 40 | 50 | 2000
Chemistry | Multiple choice | 40 | 50 | 2000
Biology | Multiple choice | 40 | 50 | 2000
History | Multiple choice | 40 | 50 | 2000
Geography | Multiple choice | 40 | 50 | 2000
Civic Education | Multiple choice | 40 | 50 | 2000

Dataset folder

    .
    ├── eval set
    │    ├── VNHSGE-V                            # Vietnamse versions
    │    │   ├── JSON format                     # JSON folder
    │    │   │     ├── Mathematics               # VNHSGE mathematcis dataset
    │    │   │     │   ├── MET_Math_IE_2023.json # JSON file     
    │    │   │     │   ├── MET_Math_IE_2023      # Image folder
    │    │   │     ├── ..........                # 
    │    │   │     ├── Civic Education           # VNHSGE civic education dataset
    │    │   ├── Word format                     # Word folder
    │    │   │     ├── Mathematics               # VNHSGE mathematcis dataset
    │    │   │     │   ├── MET_Math_IE_2023.docx # Word file 
    │    │   │     ├── ..........                # 
    │    │   │     ├── Civic Education           # VNHSGE civic education dataset
    │    └── VNHSGE-E                            # English versions
    │        ├── JSON format 
    │        ├── .............
    ├── test set
    ├── train set


Word format

| ID | IQ | Q | C | IA | E |
|---|---|---|---|---|---|
| 1 |  | The volume of a cube with edge 2a is:  A. $8a^3$  B. $2a^3$  C. $a^3$  D. $6a^3$ | A |  | The volume of a cube with edge 2a is:   $V=(2a)^3=8a^3$ |

ID refers to the ID of the question; IQ refers to the images of the question; Q refers to the question content; C refers to the choice options; IE refers to the images of the explanation; and E refers to the explanation content.

JSON format

    { 
        "ID": "1", 
        "IQ": " ", 
        "Q": "1) The volume of a cube with edge 2a is:\nA. 8a^3.\t\nB. 2a^3.\t\nC. a^3.\t\nD. 6a^3.", "C": "A", 
        "IA": " ", 
        "E": "The volume of a cube with edge 2a is: V=(2a)^3=8a^3.",
    }

<!-- LLMs Performance -->
## ChatGPT and Bing AI Chat Performances
* Response

JSON format

    { 
        "ID": "1", 
        "IQ": " ", 
        "Q": "1) The volume of a cube with edge 2a is:\nA. 8a^3.\t\nB. 2a^3.\t\nC. a^3.\t\nD. 6a^3.", "C": "A", 
        "IA": " ", 
        "E": "The volume of a cube with edge 2a is: V=(2a)^3=8a^3.", 
        "CC": "A", 
        "CE": "The formula for the volume of a cube is V = s^3, where s is the length of one of its sides. Therefore, the volume of the
    cube with a side length of 2a is: V = (2a)^3 = 8a^3", 
    }

* Performance

We evaluated the performance of ChatGPT and BingChat on the VNHSGE dataset. 

|  | Math ChatGPT | Math BingChat | Lit ChatGPT | Lit BingChat | Eng ChatGPT | Eng BingChat | Phy ChatGPT | Phy BingChat | Che ChatGPT | Che BingChat | Bio ChatGPT | Bio BingChat | His ChatGPT | His BingChat | Geo ChatGPT | Geo BingChat | Civ ChatGPT | Civ BingChat |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 2019 | 52 | 56 | 75 | 52.75 | 76 | 92 | 60 | 55 | 40 | 55 | 60 | 67.5 | 42.5 | 82.5 | 50 | 75 | 60 | 75 |
| 2020 | 66 | 56 | 68.9 | 51.25 | 86 | 96 | 62.5 | 67.5 | 42.5 | 57.5 | 60 | 72.5 | 47.5 | 85 | 52.5 | 70 | 70 | 87.5 |
| 2021 | 60 | 66 | 75 | 60.25 | 76 | 86 | 60 | 67.5 | 62.5 | 50 | 52.5 | 67.5 | 55 | 90 | 75 | 82.5 | 62.5 | 92.5 |
| 2022 | 62 | 60 | 56.3 | 70 | 80 | 94 | 65 | 67.5 | 47.5 | 47.5 | 57.5 | 72.5 | 60 | 92.5 | 62.5 | 85 | 82.5 | 90 |
| 2023 | 54 | 62 | 64.8 | 49.75 | 78 | 94 | 57.5 | 72.5 | 47.5 | 52.5 | 60 | 65 | 77.5 | 92.5 | 67.5 | 85 | 77.5 | 82.5 |
| AVG | 58.8 | 60 | 68 | 56.8 | 79.2 | 92.4 | 61 | 66 | 48 | 52.8 | 58 | 69 | 56.5 | 88.5 | 61.5 | 79.5 | 70.5 | 85.5 | 


For complex calculation and reasoning subjects like mathematics, physics, chemistry, and biology, ChatGPT and BingChat have performance ranges from 48% to 69%. However, for subjects that rely more on language skills, such as literature, English, history, geography, and civic education, their performances range from 56.5% to 92.4%.

![alt text](https://github.com/Xdao85/VNHSGE/blob/main/Figures/Performance.png?raw=true)

* Comparison of performances among ChatGPT, BingChat, and Vietnamese students in score spectrum: Our objective is to assess whether LLMs have capabilities comparable to human-level performance, despite the challenges posed by different settings. Through this comparison, we can evaluate the potential of LLMs as effective learning support tools for students across various subject areas.
![alt text](https://github.com/Xdao85/VNHSGE/blob/main/Figures/Vietnamese_student_score_spectrum.png?raw=true)

<!-- CITATION -->
## Citation

If you find this work useful for your research, please feel free to use them (don't forget to cite our paper):

```bibtex
@article{dao2023vnhsge,
  title={VHSGE: Vietnamese High School Graduation Examination Dataset for Large Language Models},
  author={Xuan-Quy Dao, Ngoc-Bich Le, The-Duy Vo, Xuan-Dung Phan, Bac-Bien Ngo, Van-Tien Nguyen, Thi-My-Thanh Nguyen},
  year={2023}
}
```

