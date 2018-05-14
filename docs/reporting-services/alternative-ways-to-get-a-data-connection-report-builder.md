---
title: 데이터에 연결하는 다른 방법(보고서 작성기) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: aebc5f3d-97d5-4d54-b525-753fed073a9a
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8d84cb434338e8174fe74f7466be768bc344e2fd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="alternative-ways-to-get-a-data-connection-report-builder"></a>데이터에 연결하는 다른 방법(보고서 작성기)
데이터 연결은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스와 같은 외부 데이터 원본에 연결하는 데 필요한 정보를 포함합니다. 일반적으로 데이터 원본 소유자로부터 사용할 자격 증명 유형과 연결 정보를 가져옵니다.  
  
데이터 연결을 지정하기 위해 보고서 서버의 공유 데이터 원본을 사용하거나 특정 보고서에만 사용되는 포함된 데이터 원본을 만들 수 있습니다.  
  
대부분의 자습서에서 포함된 데이터 원본을 사용하지만 공유 데이터 원본에 액세스할 수 있는 경우 공유 데이터 원본을 사용할 수 있습니다.  
  
## <a name="getting-a-data-connection-from-a-shared-data-source"></a>공유 데이터 원본에서 데이터 연결 가져오기  
보고서 서버에 사용할 권한이 있는 사용 가능한 공유 데이터 원본이 있는 경우 포함된 데이터 원본 대신 이 데이터 원본을 사용할 수 있습니다. 다음 절차에서는 공유 데이터 원본을 찾고 이 원본을 사용하는 데 필요한 자격 증명을 제공하는 방법을 설명합니다.  
  
공유 데이터 원본을 사용하려면 보고서 서버를 찾아 선택합니다. 일반적으로 보고서 서버 관리자가 보고서 서버 URL을 제공합니다.  
  
### <a name="to-specify-a-data-connection-from-a-list-of-shared-data-sources"></a>공유 데이터 원본 목록을 사용하여 데이터 연결을 지정하려면  
  
1.  새 테이블 또는 행렬 또는 새 차트 마법사의 **데이터 집합 선택** 페이지에서 **데이터 집합 만들기**를 선택하고 **다음**을 클릭합니다. **데이터 원본에 대한 연결 선택** 페이지가 열립니다.  
  
2.  데이터 원본 목록에서 액세스할 권한이 있는 데이터 원본을 선택합니다.  
  
3.  데이터 원본에 연결할 수 있는지 확인하려면 **연결 테스트**를 클릭합니다. "연결되었습니다."라는 메시지가 나타납니다. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  **다음**을 클릭합니다.  
  
    필요한 경우 자격 증명을 입력합니다. 자격 증명을 로컬로 저장하려면 **연결과 함께 암호 저장**을 선택합니다. 이 옵션을 선택하지 않으면 보고서를 실행할 때마다 자격 증명을 입력하라는 메시지가 표시됩니다.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-specify-a-data-connection-by-browsing-to-a-shared-data-source-on-a-report-server"></a>보고서 서버에서 공유 데이터 원본을 찾아 데이터 연결을 지정하려면  
  
1.  새 테이블 또는 행렬 또는 새 차트 마법사의 **데이터 집합 선택** 페이지에서 **데이터 집합 만들기**를 선택하고 **다음**을 클릭합니다. **데이터 원본에 대한 연결 선택** 페이지가 열립니다.  
  
2.  **찾아보기**를 클릭합니다. **데이터 원본 선택** 대화 상자가 열립니다.  
  
3.  **찾는 위치** 드롭다운 목록에서 **최근에 사용한 사이트 및 서버**를 선택합니다. 데이터 원본 창에서 서버의 URL을 클릭한 다음 **열기**를 클릭합니다.  
  
    데이터 원본 또는 모델 목록이 나타납니다.  
  
4.  또는 **이름**에 보고서 서버의 URL을 입력합니다. **열기**를 클릭합니다.  
  
    보고서 작성기가 보고서 서버에 연결하고 루트 폴더에서 사용할 수 있는 데이터 원본을 로드합니다.  
  
5.  연결할 수 있는 권한이 있는 데이터 원본이 포함된 폴더로 이동하고 데이터 원본을 선택한 다음 **열기**를 클릭합니다.  
  
    **데이터 원본에 대한 연결 선택** 페이지로 돌아갑니다.  
  
6.  데이터 원본에 연결할 수 있는지 확인하려면 **연결 테스트**를 클릭합니다.  
  
    "연결되었습니다."라는 메시지가 나타납니다. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  **다음**을 클릭합니다.  
  
8.  사용자 이름과 암호를 입력하라는 메시지가 표시되면 자격 증명을 입력합니다. 자격 증명을 로컬로 저장하려면 **연결과 함께 암호 저장**을 선택합니다.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
[보고서 데이터 집합&#40;SSRS&#41;](../reporting-services/report-data/report-datasets-ssrs.md)  
[보고서 작성기 자습서](../reporting-services/report-builder-tutorials.md) 
  

