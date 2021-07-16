

# CNN을 이용한 흉부 X-ray 영상에서의 COVID-19 및 폐렴 분류

2020년 8~12월까지 진행했던 학사학위 논문 연구이다.



## Purpose

2019년 12월, SARS-CoV-2의 감염증인 COVID-19 감염증이 전세계적으로 범유행을  일으키며 큰 영향을 끼치고 있다. COVID-19 감염증은 엄청난 수의 사망자와 환자가  발생했으며, 경제적으로도 큰 타격을 주었다. COVID-19 감염증에 걸리면 폐렴 증상을  보이기 때문에 다른 폐렴과 혼동될 수 있다. 따라서 rRT-PCR로 진단을 하는데, 이 는 전용 특수 장비가 필요하고 병의 진단에도 24시간 정도 시간이 걸린다. 때문에 모든 사람에게 적용할 수 없고 질병의 증상을 보이는 사람들에게만 적용할 수밖에 없다. 하지만 COVID-19 감염증은 증상의 정도가 개개인마다 천차만별이며, 무증상자도 있다. 게다가 전염성도 높고 백신도 완성되지 않아 빠른 진단으로 미리 예방하는 것이  최선이다. COVID-19 감염증 환자의 흉부 X-ray 영상은 폐혈관 외곽의 ground glass 패턴과 비대칭 patch, air space의 불투명도가 확산되는 특징을 보이기 때문에 폐 질환을  진단하는데 용이하다. 게다가 rRT-PCR보다 정확하고 빠르게 COVID-19 감염증을  진단할 수 있기 때문에 CNN을 통한 영상 분류로 COVID-19 감염증의 확산을 미리 예방하고 신속한 진단을 가능하게 한다.



## Datasets

Kaggle의 dataset을 이용해 연구를 진행했다.

- Dataset 출처
  - [Kaggle \- Praveen, "CoronaHack -Chest X-Ray-Dataset"]([CoronaHack -Chest X-Ray-Dataset | Kaggle](https://www.kaggle.com/praveengovi/coronahack-chest-xraydataset))
  - [Kaggle \- Nabeel Sajid, "COVID-19 Patients Lungs X Ray Images 10000"]([COVID-19 Patients Lungs X Ray Images 10000 | Kaggle](https://www.kaggle.com/nabeelsajid917/covid-19-x-ray-10000-images?select=dataset))



모든 Data는 jpg 파일이며, 크기는 일정하지 않다.

- Train Data

  - Total: 5,514

    - Pneumonia: 3,418

    - Normal: 1,266
    - COVID-19: 530

    

- Test Data
  - Total: 1,288
    - Pneumonia: 855
    - Normal: 317
    - COVID-19: 116



### Prevent bias

Trainng 과정에서 data bias(데이터 편향)을 막기 위해 각 class별 train data의 수를 통일시켜 training에 사용한다. 따라서, train data의 class 별 data의 수는 530개로 같아진다.

```python
data_cnt = []

data_cnt.append(len(Pn_images))
data_cnt.append(len(Norm_images))
data_cnt.append(len(COVID_images))

min_class = min(data_cnt) # 가장 작은 class의 data 수

# 해당 개수로 data를 random하게 추출
Pn_images = random.sample(Pn_images, min_class)
Norm_images = random.sample(Norm_images, min_class)
COVID_images = random.sample(COVID_images, min_class)
```



