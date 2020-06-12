---
title: 오류 구성 (마이닝 구조 대화 상자) (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.miningstructuredialog.general.f1
ms.assetid: d9aa028b-bad9-49c7-a81c-c2150e4dd481
author: minewiskan
ms.author: owend
ms.openlocfilehash: ef6ba1926d23990399be8571ed117b87dd2edb8b
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528388"
---
# <a name="error-configuration-mining-structure-dialog-box-analysis-services---multidimensional-data"></a>오류 구성(마이닝 구조 대화 상자)(Analysis Services - 다차원 데이터)
  **SQL Server Management Studio** 의 **마이닝 구조 속성** 대화 상자에 있는 **오류 구성** 페이지를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스의 마이닝 구조에 대한 오류 구성 속성을 설정할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **기본 오류 구성 사용**  
 처리 작업에 개체의 기본 오류 구성을 사용하려면 선택합니다.  
  
 **키 오류 동작**  
 처리 중 조회할 수 없는 새 키를 발견할 경우 다음 중에서 수행할 동작을 선택합니다.  
  
-   **알 수 없음 상태로 변환** 은 레코드 정보를 알 수 없는 멤버로 집계합니다.  
  
-   **레코드 삭제** 는 레코드 정보가 개체와 함께 처리되지 않도록 제외합니다.  
  
 **오류 개수 무시**  
 처리 중 발생한 오류를 무시하려면 클릭합니다.  
  
 **오류 발생 시 중지**  
 오류 발생 시 처리를 중지하려면 클릭합니다. 이 옵션을 사용하면 **오류 개수** 및 **오류 시 수행할 동작** 옵션이 활성화됩니다.  
  
 **오류 개수**  
 처리를 중지할 때까지 무시할 오류 수를 입력합니다.  
  
 **오류 시 수행할 동작**  
 다음 동작 중에서 오류 수가 **오류 개수**의 값을 초과할 경우 수행할 작업을 선택합니다.  
  
-   **처리 중지** 는 처리 작업을 종료합니다.  
  
-   **로깅 중지** 는 오류 기록은 중지하지만 처리 작업은 계속합니다.  
  
 **키를 찾을 수 없는 경우**  
 다음 동작 중에서 개체 처리 시 키가 없을 경우 수행할 작업을 지정합니다.  
  
-   오류 **무시** 는 오류를 무시 합니다.  
  
-   **보고서 및 계속** 에서 오류를 보고 하 고 처리 작업을 계속 합니다.  
  
-   **보고하고 중지** 는 오류를 보고하고 처리 작업을 중지합니다.  
  
 **중복 키**  
 다음 동작 중에서 개체 처리 시 중복 키가 있을 경우 수행할 작업을 지정합니다.  
  
-   오류 **무시** 는 오류를 무시 합니다.  
  
-   **보고서 및 계속** 에서 오류를 보고 하 고 처리 작업을 계속 합니다.  
  
-   **보고하고 중지** 는 오류를 보고하고 처리 작업을 중지합니다.  
  
 **Null 키가 알 수 없음으로 변환 되었습니다.**  
 다음 동작 중에서 개체 처리 시 알 수 없는 멤버에 Null 멤버 키를 추가한 경우 수행할 작업을 지정합니다.  
  
-   오류 **무시** 는 오류를 무시 합니다.  
  
-   **보고서 및 계속** 에서 오류를 보고 하 고 처리 작업을 계속 합니다.  
  
-   **보고하고 중지** 는 오류를 보고하고 처리 작업을 중지합니다.  
  
 **Null 키가 허용 되지 않습니다.**  
 다음 동작 중에서 개체 처리 시 허용되지 않는 Null 키를 발견한 경우 수행할 작업을 지정합니다.  
  
-   오류 **무시** 는 오류를 무시 합니다.  
  
-   **보고서 및 계속** 에서 오류를 보고 하 고 처리 작업을 계속 합니다.  
  
-   **보고하고 중지** 는 오류를 보고하고 처리 작업을 중지합니다.  
  
 **오류 로그 경로**  
 오류 로그 파일의 전체 경로 및 파일 이름을 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [마이닝 구조 속성 대화 &#40;Analysis Services 데이터 마이닝&#41;](mining-structure-properties-dialog-analysis-services-data-mining.md)   
 [일반 &#40;마이닝 구조 대화 상자&#41; &#40;Analysis Services 데이터 마이닝&#41;](general-mining-structure-dialog-box-analysis-services-data-mining.md)  
  
  
