---
title: 마이닝 모델 문서화 (Excel 용 데이터 마이닝 추가 기능) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- documenting models
- mining structures, managing
- mining models, managing
- model properties
ms.assetid: 0a663e11-e40c-4708-ad18-fabb6c976fa4
author: minewiskan
ms.author: owend
ms.openlocfilehash: 92ed5c43fa2b7484485b915d42946121487386d9
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528489"
---
# <a name="documenting-mining-models-data-mining-add-ins-for-excel"></a>마이닝 모델 문서화(Excel용 데이터 마이닝 추가 기능)
  ![데이터 마이닝 리본, 모델 문서화 단추](media/dmc-docmodel.gif "데이터 마이닝 리본, 모델 문서화 단추")  
  
 **모델 문서화** 마법사는 사용자가 만든 마이닝 모델에 대 한 유용한 정보를 제공 하는 보고서를 만듭니다. 만드는 모델을 문서화하면 모델을 생성하는 데 사용한 데이터 원본을 추적하고, 모델이 처리된 시점에 대한 추가 정보를 가져오고, 모델의 결과에 영향을 주는 매개 변수 변경을 추적할 수 있습니다.  
  
## <a name="using-the-document-model-wizard"></a>모델 문서화 마법사 사용  
  
1.  **데이터 마이닝** 탭을 클릭 합니다.  
  
2.  **모델 사용** 그룹에서 **모델 문서화**를 클릭 합니다.  
  
3.  **모델 선택** 대화 상자에서 보고할 모델을 선택 하 고 **다음**을 클릭 합니다. 문서화 하려는 각 모델에 대해 **모델 문서화** 마법사를 별도로 실행 해야 합니다.  
  
4.  **문서 세부 정보 선택** 대화 상자에서 다음 두 가지 옵션 중 하나를 선택 합니다. **전체 정보** 또는 **요약 정보**  
  
5.  **Finish**를 클릭합니다.  
  
6.  마법사가 지정 된 보고서 ( **모델 설명서**)를 포함 하는 새 워크시트를 자동으로 만듭니다.  
  
## <a name="understanding-the-report"></a>보고서 이해  
 데이터 마이닝 모델을 문서화하는 보고서를 만들 때 모델의 이름 및 설명 등의 기본 정보가 포함된 요약 보고서를 만들거나 마이닝 모델의 기본 구조 및 고급 정보에 대한 세부 사항이 포함된 전체 보고서를 만들 수 있습니다.  
  
 모델을 만드는 데 사용한 알고리즘에 따라 다른 유형의 정보가 제공됩니다. 예를 들어 연결 모델에서는 생성된 항목 집합 및 규칙의 수를 확인하는 것이 중요하고, 클러스터링 모델에서는 클러스터의 수가 더 중요할 수 있습니다.  
  
 다음 표에서는 각 옵션의 보고서에서 제공되는 옵션 및 정보를 나열합니다.  
  
> [!NOTE]  
>  보고서의 열은 기본적으로 특정 크기로 설정됩니다. 따라서 열 이름 또는 값이 매우 길면 Excel에 표시되지 않거나 ###으로 나타날 수 있습니다. 행의 크기를 조정하여 값을 표시할 수 있습니다. 셀을 선택한 다음 수식 입력줄의 오른쪽 끝에서 이중 화살표를 클릭한 상태로 끌어 전체 값 또는 문자열을 표시할 수 있습니다.  
  
### <a name="summary-report"></a>요약 보고서  
  
||||  
|-|-|-|  
|**메타데이터**|모델 이름<br /><br /> 모델 설명<br /><br /> 알고리즘 이름<br /><br /> 마지막 처리 날짜||  
|**모델 결과**|연결|항목 집합 수<br /><br /> 규칙 수|  
||Clustering|클러스터 수<br /><br /> 각 클러스터 지원|  
||의사 결정 트리|트리 수<br /><br /> 각 트리의 노드 수|  
||선형 회귀|트리 수(항상 1)<br /><br /> 노드 수(항상 1)|  
||Naïve Bayes|중요한 특성|  
||신경망|입력 노드 수<br /><br /> 출력 노드 수<br /><br /> 숨겨진 노드 수|  
||시퀀스 클러스터링|클러스터 수|  
  
### <a name="complete-report"></a>전체 보고서  
 전체 보고서에는 요약 보고서의 모든 내용과 모델에 사용된 데이터 열 및 분석 결과에 대한 세부 정보가 포함되어 있습니다.  
  
||||  
|-|-|-|  
|**메타데이터**|모델 메타데이터|알고리즘 매개 변수 및 값|  
||열 메타데이터|열 이름<br /><br /> 사용<br /><br /> 데이터 형식<br /><br /> 내용 유형<br /><br /> 값(불연속 값 목록 또는 값 범위)|  
|**모델 통계**|연속 열|평균값<br /><br /> 최소값<br /><br /> 최대값<br /><br /> 제곱 평균 오차<br /><br /> 절대 평균 오차<br /><br /> 로그 점수<br /><br /> 회귀 수식(선형 회귀 모델만 해당)|  
||불연속 열|전달 횟수<br /><br /> 실패 횟수<br /><br /> 로그 점수<br /><br /> 리프트|  
  
> [!NOTE]  
>  SQL Server Analysis Services에서 지원하는 모든 모델 유형은 문서화할 수 있습니다. 따라서 테이블 분석 도구 또는 데이터 마이닝 클라이언트의 마법사를 통해 만들 수 없는 일부 모델 유형만 표에 나열되어 있습니다. 그러나 **고급 데이터 마이닝 쿼리 편집기**를 사용 하 여 모든 모델 유형을 만들 수 있습니다. 자세한 내용은 [쿼리 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](query-sql-server-data-mining-add-ins.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Excel 용 데이터 마이닝 추가 기능 &#40;마이닝 모델 배포 및 확장&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
