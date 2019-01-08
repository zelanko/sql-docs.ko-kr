---
title: Analysis Services 테이블 형식 모델에서 역할 만들기 및 관리 | Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 093197db8257cf9be261658f1828783fa01d7cc2
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072220"
---
# <a name="create-and-manage-roles"></a>역할 만들기 및 관리 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  테이블 형식 모델에서 역할은 모델에 대한 멤버 권한을 정의합니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 역할 관리자 대화 상자를 사용하여 모델 프로젝트에 대해 역할을 정의합니다. 

> [!IMPORTANT]
> Azure Analysis Services에 프로젝트를 배포 하는 경우 사용 **통합 작업 영역** 작업 영역 데이터베이스로 합니다. 자세한 내용은 참조 하세요 [작업 영역 데이터베이스](workspace-database-ssas-tabular.md)합니다.
  
 이 문서의 작업을 만들고 역할에서 역할 관리자 대화 상자를 사용 하 여 모델 제작 중에 관리 하는 방법을 설명 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]합니다. 배포 된 model 데이터베이스에서 역할을 관리 하는 방법에 대 한 내용은 [테이블 형식 모델 역할](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md)입니다.  
  
## <a name="tasks"></a>태스크  
 역할을 만들고, 편집, 복사 및 삭제하려면 **역할 관리자** 대화 상자를 사용합니다. **역할 관리자** 대화 상자를 보려면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **역할 관리자**를 클릭합니다.  
  
###  <a name="bkmk_new_role"></a> 새 역할을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **역할 관리자**를 클릭합니다.  
  
2.  **역할 관리자** 대화 상자에서 **새로 만들기**를 클릭합니다.  
  
     강조 표시된 새 역할이 역할 목록에 추가됩니다.  
  
3.  **역할** 목록의 **이름** 필드에 역할의 이름을 입력합니다.  
  
     기본적으로 기본 역할의 이름은 새 역할을 만들 때마다 증분식으로 번호가 지정됩니다. 따라서 재무 관리자 또는 인적 자원 전문가와 같이 멤버 유형을 분명하게 식별하는 이름을 입력하는 것이 좋습니다.  
  
4.  **사용 권한** 필드에서 아래쪽 화살표를 클릭하고 다음 사용 권한 유형 중 하나를 선택합니다.  
  
    |사용 권한|Description|  
    |----------------|-----------------|  
    |**없음**|멤버는 모델 스키마를 수정할 수 없으며 데이터를 쿼리할 수 없습니다.|  
    |**읽기**|멤버는 행 필터를 기반으로 데이터를 쿼리할 수 있지만 모델 스키마를 변경할 수 없습니다.|  
    |**읽기 및 처리**|멤버는 행 수준 필터를 기반으로 데이터를 쿼리하고 처리 및 모두 처리 작업을 실행할 수 있지만 모델 스키마를 변경할 수 없습니다.|  
    |**처리**|멤버는 처리 및 모두 처리 작업을 실행할 수 있습니다. 모델 스키마를 수정할 수 없으며 데이터를 쿼리할 수 없습니다.|  
    |**관리자**|멤버는 모델 스키마를 수정할 수 있으며 모든 데이터를 쿼리할 수 있습니다.|  
  
5.  역할에 대한 설명을 입력하려면 **설명** 필드를 클릭한 다음 설명을 입력합니다.  
  
6.  만들고 있는 역할에 읽기 또는 읽기 및 처리 권한이 있는 경우 DAX 수식을 사용하여 행 필터를 추가할 수 있습니다. 행 필터를 추가하려면 **행 필터** 탭을 클릭하고 테이블을 선택한 다음 **DAX 필터** 필드를 클릭하고 DAX 수식을 입력합니다.  
  
7.  멤버를 역할에 추가하려면 **멤버** 탭을 클릭한 다음 **추가**를 클릭합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 역할 멤버를 배포된 모델에 추가할 수도 있습니다. 자세한 내용은 [SSMS를 사용 하 여 역할 관리](../../analysis-services/tabular-models/manage-roles-by-using-ssms-ssas-tabular.md)합니다.  
  
8.  **사용자 또는 그룹 선택** 대화 상자에서 Windows 사용자 또는 Windows 그룹 개체를 멤버로 입력합니다.  
  
9. **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고자료  
 [역할](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [큐브 뷰](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Excel에서 분석](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)   
 [USERNAME 함수(DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f)   
 [CUSTOMDATA 함수(DAX)](http://msdn.microsoft.com/58235ad8-226c-43cc-8a69-5a52ac19dd4e)  
  
  
