---
title: '자습서: Python에서 모델을 빌드하여 고객 범주화'
description: 네 부분으로 구성 된 자습서 시리즈의 3 부에서는 SQL Server Machine Learning Services를 사용 하 여 Python에서 클러스터링을 수행 하는 K 수단 모델을 작성 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8707d14b1e332ae6ecebf83213ed53701343bcd3
ms.sourcegitcommit: 26715b4dbef95d99abf2ab7198a00e6e2c550243
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70294408"
---
# <a name="tutorial-build-a-model-in-python-to-categorize-customers-with-sql-server-machine-learning-services"></a>자습서: SQL Server를 사용 하 여 고객을 범주화 하는 모델을 Python에서 작성 Machine Learning Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

네 부분으로 구성 된 자습서 시리즈의 3 부에서는 클러스터링을 수행 하기 위해 Python에서 K를 의미 하는 모델을 작성 합니다. 이 시리즈의 다음 부분에서는 SQL Server Machine Learning Services를 사용 하 여이 모델을 SQL database에 배포 합니다.

이 문서에서는 다음 방법을 설명합니다.

> [!div class="checklist"]
> * K를 의미 하는 알고리즘에 대 한 클러스터 수를 정의 합니다.
> * 클러스터링 수행
> * 결과 분석

[1 부](python-clustering-model.md)에서는 필수 구성 요소를 설치 하 고 샘플 데이터베이스를 복원 했습니다.

[2 부](python-clustering-model-prepare-data.md)에서는 클러스터링을 수행 하기 위해 SQL database에서 데이터를 준비 하는 방법을 배웠습니다.

[4 부](python-clustering-model-deploy.md)에서는 새 데이터를 기반으로 Python에서 클러스터링을 수행할 수 있는 SQL 데이터베이스에 저장 프로시저를 만드는 방법에 대해 알아봅니다.

## <a name="prerequisites"></a>사전 요구 사항

* 이 자습서의 3 부에서는 [**1**](python-clustering-model.md)부의 전제 조건을 충족 했으며 [**2 부**](python-clustering-model-prepare-data.md)의 단계를 완료 했다고 가정 합니다.

## <a name="define-the-number-of-clusters"></a>클러스터 수를 정의 합니다.

고객 데이터를 클러스터링 하려면 데이터를 그룹화 하는 가장 간단 하 고 잘 알려진 방법 중 하나인 **K-** 를 사용 하는 클러스터링 알고리즘을 사용 합니다.
K에 대 한 자세한 내용은 K-에 대 한 [전체 가이드 클러스터링 알고리즘을](https://www.kdnuggets.com/2019/05/guide-k-means-clustering-algorithm.html)참조 하세요.

이 알고리즘은 두 가지 입력을 허용 합니다. 데이터 자체 및 생성할 클러스터 수를 나타내는 미리 정의 된 숫자 "*k*"
출력은 클러스터 간에 분할 된 입력 데이터를 사용 하는 *k* 클러스터입니다.

K의 목표는 동일한 클러스터의 모든 항목이 서로 유사 하 고 가능한 한 다른 클러스터의 항목과 다른 항목을 k 클러스터로 그룹화 하는 것입니다.

사용할 알고리즘의 클러스터 수를 확인 하려면 추출 된 클러스터 수 별 제곱의 합계에서 그림을 사용 합니다. 사용할 적절 한 클러스터 수는 플롯의 벤드 또는 "엘 보"에 있습니다.

```python
################################################################################################
## Determine number of clusters using the Elbow method
################################################################################################

cdata = customer_data
K = range(1, 20)
KM = (sk_cluster.KMeans(n_clusters=k).fit(cdata) for k in K)
centroids = (k.cluster_centers_ for k in KM)

D_k = (sci_distance.cdist(cdata, cent, 'euclidean') for cent in centroids)
dist = (np.min(D, axis=1) for D in D_k)
avgWithinSS = [sum(d) / cdata.shape[0] for d in dist]
plt.plot(K, avgWithinSS, 'b*-')
plt.grid(True)
plt.xlabel('Number of clusters')
plt.ylabel('Average within-cluster sum of squares')
plt.title('Elbow for KMeans clustering')
plt.show()
```

![엘 보 그래프](./media/python-tutorial-elbow-graph.png)

그래프에 따라 *k = 4* 가 시도 하는 것과 같습니다. 이 *k* 값은 고객을 4 개의 클러스터로 그룹화 합니다.

## <a name="perform-clustering"></a>클러스터링 수행

다음 Python 스크립트에서는 KMeans package 패키지의 KMeans 함수를 사용 합니다.

```python
################################################################################################
## Perform clustering using Kmeans
################################################################################################

# It looks like k=4 is a good number to use based on the elbow graph.
n_clusters = 4

means_cluster = sk_cluster.KMeans(n_clusters=n_clusters, random_state=111)
columns = ["orderRatio", "itemsRatio", "monetaryRatio", "frequency"]
est = means_cluster.fit(customer_data[columns])
clusters = est.labels_
customer_data['cluster'] = clusters

# Print some data about the clusters:

# For each cluster, count the members.
for c in range(n_clusters):
    cluster_members=customer_data[customer_data['cluster'] == c][:]
    print('Cluster{}(n={}):'.format(c, len(cluster_members)))
    print('-'* 17)
print(customer_data.groupby(['cluster']).mean())
```

## <a name="analyze-the-results"></a>결과 분석

이제 K를 사용 하 여 클러스터링을 수행 했으므로 다음 단계는 결과를 분석 하 고 조치 가능한 정보를 찾을 수 있는지 확인 하는 것입니다.

이전 스크립트에서 인쇄 된 클러스터링 평균 값 및 클러스터 크기를 확인 합니다.

```results
Cluster0(n=31675):
-------------------
Cluster1(n=4989):
-------------------
Cluster2(n=1):
-------------------
Cluster3(n=671):
-------------------

         customer  orderRatio  itemsRatio  monetaryRatio  frequency
cluster
0        50854.809882    0.000000    0.000000       0.000000   0.000000
1        51332.535779    0.721604    0.453365       0.307721   1.097815
2        57044.000000    1.000000    2.000000     108.719154   1.000000
3        48516.023845    0.136277    0.078346       0.044497   4.271237
```

4 개의 클러스터는 [1 부](python-clustering-model-prepare-data.md#separate-customers)에 정의 된 변수를 사용 하 여 제공 됩니다.

* *orderRatio* = 반환 주문 비율 (전체 주문 수와 부분적으로 또는 완전히 반환 된 총 주문 수)
* 항목 *비율* = 반환 항목 비율 (반환 된 항목의 총 수 및 구매한 항목 수와 비교)
* *Monetaryratio* = 반환 금액 비율 (반환 된 항목의 총 금액 및 구매한 금액)
* *frequency* = 반환 빈도

K를 사용 하 여 데이터 마이닝은 결과를 추가로 분석 해야 하 고, 각 클러스터를 보다 잘 이해 하기 위해 추가 단계를 수행 해야 하지만 좋은 리드를 제공할 수 있습니다.
이러한 결과를 해석할 수 있는 몇 가지 방법은 다음과 같습니다.

* 클러스터 0은 활성 상태가 아닌 고객 그룹인 것 같습니다 (모든 값이 0).
* 클러스터 3은 반환 동작을 기준으로 하는 그룹으로 보입니다.

클러스터 0은 명확 하 게 활성 상태가 아닌 고객 집합입니다. 아마도이 그룹에 대 한 마케팅 활동을 대상으로 하 여 구매에 관심을 트리거할 수 있습니다. 다음 단계에서는 마케팅 전자 메일을 보낼 수 있도록 데이터베이스에 클러스터 0의 고객 전자 메일 주소를 쿼리 합니다.

## <a name="clean-up-resources"></a>리소스 정리

이 자습서를 계속 진행 하지 않으려면 SQL Server에서 tpcxbb_1gb 데이터베이스를 삭제 하세요.

## <a name="next-steps"></a>다음 단계

이 자습서 시리즈의 3 부에서는 다음 단계를 완료 했습니다.

* K를 의미 하는 알고리즘에 대 한 클러스터 수를 정의 합니다.
* 클러스터링 수행
* 결과 분석

만든 machine learning 모델을 배포 하려면이 자습서 시리즈의 4 부를 따르세요.

> [!div class="nextstepaction"]
> [자습서: SQL Server Machine Learning Services를 사용 하 여 Python에 클러스터링 모델 배포](python-clustering-model-deploy.md)