---
title: 역할 만들기 및 관리 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.rolemanager.f1
- sql12.asvs.bidtoolset.roledb.f1
ms.assetid: e23d27a8-e968-4082-9dbe-963fc724b5d9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 10e5e26142cd1819e4f2c5f884af9c2f2af10812
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67284899"
---
# <a name="create-and-manage-roles-ssas-tabular"></a>역할 만들기 및 관리(SSAS 테이블 형식)
  테이블 형식 모델에서 역할은 모델에 대한 멤버 권한을 정의합니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 역할 관리자 대화 상자를 사용하여 모델 프로젝트에 대해 역할을 정의합니다. 모델을 배포할 때 데이터베이스 관리자는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 역할을 관리할 수 있습니다.  
  
 이 항목의 태스크에서는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 역할 관리자 대화 상자를 사용하여 모델 제작 중에 역할을 만들고 관리하는 방법을 설명합니다. 배포된 model 데이터베이스에서 역할을 관리하는 방법은 [테이블 형식 모델 역할&#40;SSAS 테이블 형식&#41;](roles-ssas-tabular.md)을 참조하세요.  
  
## <a name="tasks"></a>작업  
 역할을 만들고, 편집, 복사 및 삭제하려면 **역할 관리자** 대화 상자를 사용합니다. **역할 관리자** 대화 상자를 보려면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **역할 관리자**를 클릭합니다.  
  
###  <a name="to-create-a-new-role"></a><a name="bkmk_new_role"></a>새 역할을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **역할 관리자**를 클릭합니다.  
  
2.  **역할 관리자** 대화 상자에서 **새로 만들기**를 클릭합니다.  
  
     강조 표시된 새 역할이 역할 목록에 추가됩니다.  
  
3.  **역할** 목록의 **이름** 필드에 역할의 이름을 입력합니다.  
  
     기본적으로 기본 역할의 이름은 새 역할을 만들 때마다 증분식으로 번호가 지정됩니다. 따라서 재무 관리자 또는 인적 자원 전문가와 같이 멤버 유형을 분명하게 식별하는 이름을 입력하는 것이 좋습니다.  
  
4.  **사용 권한** 필드에서 아래쪽 화살표를 클릭하고 다음 사용 권한 유형 중 하나를 선택합니다.  
  
    |사용 권한|설명|  
    |----------------|-----------------|  
    |**없음**|멤버는 모델 스키마를 수정할 수 없으며 데이터를 쿼리할 수 없습니다.|  
    |**읽기**|멤버는 행 필터를 기반으로 데이터를 쿼리할 수 있지만 모델 스키마를 변경할 수 없습니다.|  
    |**읽기 및 처리**|멤버는 행 수준 필터를 기반으로 데이터를 쿼리하고 처리 및 모두 처리 작업을 실행할 수 있지만 모델 스키마를 변경할 수 없습니다.|  
    |**프로세스**|멤버는 처리 및 모두 처리 작업을 실행할 수 있습니다. 모델 스키마를 수정할 수 없으며 데이터를 쿼리할 수 없습니다.|  
    |**관리자나**|멤버는 모델 스키마를 수정할 수 있으며 모든 데이터를 쿼리할 수 있습니다.|  
  
5.  역할에 대한 설명을 입력하려면 **설명** 필드를 클릭한 다음 설명을 입력합니다.  
  
6.  만들고 있는 역할에 읽기 또는 읽기 및 처리 권한이 있는 경우 DAX 수식을 사용하여 행 필터를 추가할 수 있습니다. 행 필터를 추가하려면 **행 필터** 탭을 클릭하고 테이블을 선택한 다음 **DAX 필터** 필드를 클릭하고 DAX 수식을 입력합니다.  
  
7.  멤버를 역할에 추가하려면 **멤버** 탭을 클릭한 다음 **추가**를 클릭합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 역할 멤버를 배포된 모델에 추가할 수도 있습니다. 자세한 내용은 [SSMS를 사용하여 역할 관리&#40;SSAS 테이블 형식&#41;](manage-roles-by-using-ssms-ssas-tabular.md)를 참조하세요.  
  
8.  **사용자 또는 그룹 선택** 대화 상자에서 Windows 사용자 또는 Windows 그룹 개체를 멤버로 입력합니다.  
  
9. **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SSAS 테이블 형식&#41;역할 &#40;](roles-ssas-tabular.md)   
 [SSAS 테이블 형식&#41;&#40;큐브 뷰](perspectives-ssas-tabular.md)   
 [Excel에서 분석 &#40;SSAS 테이블 형식&#41;](analyze-in-excel-ssas-tabular.md)   
 [DAX&#41;&#40;USERNAME 함수](/dax/username-function-dax)   
 [CUSTOMDATA 함수 &#40;DAX&#41;](/dax/customdata-function-dax)  
  
  
