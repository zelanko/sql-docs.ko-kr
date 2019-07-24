---
title: '자습서: OData 원본 사용 | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2c64cf8b-5edb-48df-8ffe-697096258f71
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c88e14257630f74b168c89bc2cd8409763358f40
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113687"
---
# <a name="tutorial-using-the-odata-source"></a>자습서: OData 원본 사용

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  이 자습서에서는 샘플 **Northwind** OData 서비스(https://services.odata.org/V3/Northwind/Northwind.svc/) 에서 **Employees** 컬렉션을 추출한 다음, 플랫 파일로 로드하는 프로세스를 안내합니다.  
  
## <a name="1-create-an-integration-services-project"></a>1. Integration Services 프로젝트 만들기  
  
1.  **SQL Server Data Tools** 또는 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]를 실행합니다.  
  
2.  **파일**을 클릭하고 **새로 만들기**를 가리킨 후 **프로젝트**를 클릭합니다.  
  
3.  **새 프로젝트** 대화 상자에서 **설치됨**, **템플릿**, **비즈니스 인텔리전스**를 차례로 확장하고 **Integration Services**를 클릭합니다.  
  
4.  프로젝트 유형으로 **Integration Services 프로젝트** 를 선택합니다.  
  
5.  **이름** 을 입력하고 프로젝트의 **위치** 를 선택한 후 **확인**을 클릭합니다.  
  
## <a name="2-add-and-configure-an-odata-source"></a>2. OData 원본 추가 및 구성 
  
1.  **데이터 흐름 태스크** 를 **SSIS 도구 상자** 에서 SSIS 패키지의 제어 흐름 디자인 화면에 끌어 놓습니다.  
  
2.  **데이터 흐름** 탭을 클릭하거나 **데이터 흐름 태스크**를 두 번 클릭하여 데이터 흐름 디자인 화면을 엽니다.  
  
3.  **SSIS 도구 상자** 의 **공통** 그룹에서 **OData 원본**을 끌어 놓습니다.
  
4.  **OData 원본** 구성 요소를 두 번 클릭하여 **OData 원본 편집기** 대화 상자를 실행합니다.  
  
5.  **새로 만들기...** 를 클릭하여 새 OData 연결 관리자를 추가합니다.  
  
6.  **서비스 문서 위치**에 대해 OData 서비스 URL을 입력합니다. 이 URL은 서비스 문서나 특정 피드 또는 엔터티에 대한 URL일 수 있습니다. 이 자습서의 목적을 위해 서비스 문서에 대한 URL([https://services.odata.org/V3/Northwind/Northwind.svc/](https://services.odata.org/V3/Northwind/Northwind.svc/))을 입력합니다.  
  
7.  OData 서비스에 액세스하는 데 사용할 **인증** 으로 **Windows 인증** 이 선택되었는지 확인합니다. 기본적으로**Windows 인증** 이 선택됩니다.  
  
8.  **연결 테스트**를 클릭하여 연결을 테스트하고 **확인**을 클릭하여 OData 연결 관리자의 인스턴스 만들기를 완료합니다.  
  
9. **OData 원본 편집기** 대화 상자에서 **리소스 경로에 컬렉션 사용** 옵션에 대해 **컬렉션** 이 선택되었는지 확인합니다.  
  
10. **컬렉션** 드롭다운 목록에서 **Employees**를 선택합니다.  
  
11. **쿼리 옵션**에 대해 추가 OData 쿼리 옵션 또는 필터를 입력합니다. `$orderby=CompanyName&$top=100`)을 입력합니다. 이 자습서에서는 `$top=5`를 입력합니다.  
  
12. **미리 보기** 를 클릭해서 데이터를 미리 봅니다.  
  
13. 왼쪽 탐색 창에서 **열** 을 클릭해서 **열** 페이지로 전환합니다.  
  
14. 확인란을 선택해서 **사용 가능한 외부 열**에서 **EmployeeID**, **FirstName** 및 **LastName** 을 선택합니다.  
  
15. **확인** 을 클릭해서 **OData 원본 편집기** 대화 상자를 닫습니다.  
  
## <a name="3-add-and-configure-a-flat-file-destination"></a>3. 플랫 파일 대상 추가 및 구성
  
1.  이제 **SSIS 도구 상자** 에서 **OData 원본** 구성 요소 아래의 데이터 흐름 디자인 화면으로 **플랫 파일 대상** 을 끌어 놓습니다.  
  
2.  파란색 화살표를 사용해서 **OData 원본** 구성 요소를 **플랫 파일 대상** 구성 요소와 연결합니다.  
  
3.  **플랫 파일 대상**을 두 번 클릭합니다. **플랫 파일 대상 편집기** 대화 상자가 표시됩니다.  
  
4.  **플랫 파일 대상 편집기** 대화 상자에서 **새로 만들기** 를 클릭하여 새 플랫 파일 연결 관리자를 만듭니다.  
  
5.  **플랫 파일 형식** 대화 상자에서 **구분 기호로 분리됨**을 선택합니다. **플랫 파일 연결 관리자 편집기** 대화 상자가 표시됩니다.  
  
6.  **플랫 파일 연결 관리자 편집기** 대화 상자에서 **파일 이름**으로 `c:\Employees.txt`를 입력합니다.  
  
7.  왼쪽 탐색 창에서 **열**을 클릭합니다. 이 페이지에서 데이터를 미리 볼 수 있습니다.  
  
8.  확인을 클릭하여 **플랫 파일 연결 관리자** 편집기 대화 상자를 닫습니다.  
  
9. **플랫 파일 대상 편집기** 대화 상자에서 왼쪽 탐색 창에 있는 **매핑** 을 클릭합니다. 매핑을 검토합니다.  
  
10. 확인을 클릭하여 **플랫 파일 대상 편집기** 대화 상자를 닫습니다.  

## <a name="4-run-the-package"></a>4. 패키지 실행
SSIS 패키지를 실행합니다. OData 피드로부터 5명의 직원에 대한 ID, First Name 및 Last Name을 사용해서 출력 파일이 만들어졌는지 확인합니다.
  
  
