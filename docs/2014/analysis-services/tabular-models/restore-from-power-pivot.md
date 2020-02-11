---
title: PowerPivot에서 복원 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql11.asvs.ssmsimbi.RestoreFromPP.f1
ms.assetid: 232ac8ed-77fe-47d8-acd3-59bc2fdfdf48
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f90ea08269e79e57c623af41fc2f0fbc09e2fb42
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66066642"
---
# <a name="restore-from-powerpivot"></a>PowerPivot에서 복원
  SQL Server Management Studio의 PowerPivot 기능에서 복원을 사용하여 테이블 형식 모드에서 실행되는 Analysis Services 인스턴스에서 새 테이블 형식 model 데이터베이스를 만들거나 PowerPivot 통합 문서(.xlsx)에서 기존 데이터베이스를 복원할 수 있습니다.  
  
> [!NOTE]  
>  SQL Server Data Tools의 PowerPivot 프로젝트 템플릿에서 가져오기가 비슷한 기능을 제공합니다. 자세한 내용은 [PowerPivot에서 가져오기 &#40;SSAS 테이블 형식&#41;](import-from-power-pivot-ssas-tabular.md)을 참조 하세요.  
  
 PowerPivot에서 복원을 사용할 때는 다음 사항에 유의해야 합니다.  
  
-   PowerPivot에서 복원을 사용하려면 Analysis Services 인스턴스에서 서버 관리자 역할의 멤버로 로그인해야 합니다.  
  
-   Analysis Services 인스턴스 서비스 계정은 복원할 통합 문서 파일에 대한 읽기 권한을 가지고 있어야 합니다.  
  
-   기본적으로, PowerPivot에서 데이터베이스를 복원하는 경우 테이블 형식 model 데이터베이스 데이터 원본 가장 정보 속성이 Analysis Services 인스턴스 서비스 계정을 지정하는 기본값으로 설정됩니다. 가장 자격 증명을 데이터베이스 속성의 Windows 사용자 계정으로 변경하는 것이 좋습니다. 자세한 내용은 [가장&#40;SSAS 테이블 형식&#41;](impersonation-ssas-tabular.md)을 참조하세요.  
  
-   PowerPivot 데이터 모델의 데이터는 Analysis Services 인스턴스의 기존 또는 새 테이블 형식 model 데이터베이스로 복사됩니다. PowerPivot 통합 문서에 연결된 테이블이 있는 경우 해당 테이블은 데이터 원본을 사용하지 않고 새 테이블에 붙여넣기를 사용하여 만드는 테이블과 비슷한 테이블로 다시 만들어집니다.  
  
### <a name="to-restore-from-powerpivot"></a>PowerPivot에서 복원하려면  
  
1.  SSMS의 복원 하려는 Active Directory 인스턴스에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭 한 다음 **PowerPivot에서 복원**을 클릭 합니다.  
  
2.  
  **PowerPivot에서 복원** 대화 상자의 **복원 원본**에 있는 **백업 파일**에서 **찾아보기**를 클릭한 다음 복원할 .abf 또는 .xslx 파일을 선택합니다.  
  
3.  
  **대상 복원**의 **데이터베이스 복원**에 새 데이터베이스 또는 기존 데이터베이스의 이름을 입력합니다. 이름을 지정하지 않으면 통합 문서의 이름이 사용됩니다.  
  
4.  
  **스토리지 위치**에서 **찾아보기**를 클릭한 다음 데이터베이스를 저장할 위치를 선택합니다.  
  
5.  
  **옵션**에서 **보안 정보 포함** 을 선택합니다. PowerPivot 통합 문서에서 복원할 때 이 설정은 적용되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 형식 모델 데이터베이스 &#40;SSAS 테이블 형식&#41;](tabular-model-databases-ssas-tabular.md)   
 [PowerPivot &#40;SSAS 테이블 형식&#41;에서 가져오기](import-from-power-pivot-ssas-tabular.md)  
  
  
