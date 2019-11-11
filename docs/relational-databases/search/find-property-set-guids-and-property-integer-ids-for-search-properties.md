---
title: 검색 속성의 속성 집합 GUID 및 속성 정수 ID 찾기 | Microsoft 문서
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], configuring
ms.assetid: 7db79165-8bcc-4be6-8d40-12d44deda79f
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 94a7ad079b94d9bc34e5b0e7f7ad55393d8f5de5
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73638051"
---
# <a name="find-property-set-guids-and-property-integer-ids-for-search-properties"></a>검색 속성의 속성 집합 GUID 및 속성 정수 ID찾기
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 항목에서는 검색 속성 목록에 속성을 추가하고 전체 텍스트 검색으로 검색할 수 있도록 설정하기 전에 필요한 값을 가져오는 방법에 대해 설명합니다. 이러한 값에는 문서 속성의 속성 집합 GUID와 속성 정수 식별자가 포함됩니다.  
  
 이진 데이터에서 즉, **varbinary**, **varbinary(max)** (**FILESTREAM**포함) 또는 **image** 데이터 형식 열에 저장된 데이터에서 IFilter를 통해 추출된 문서 속성은 전체 텍스트 검색에 사용할 수 있습니다. 추출된 속성을 검색할 수 있도록 설정하려면 속성을 검색 속성 목록에 수동으로 추가해야 합니다. 또한 검색 속성 목록은 하나 이상의 전체 텍스트 인덱스와 연결되어야 합니다. 자세한 내용은 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)을 참조하세요.  
  
 사용 가능한 속성을 속성 목록에 추가하려면 먼저 속성에 대한 다음 두 가지 정보를 찾아야 합니다.  
  
-   속성의 속성 집합 GUID  
  
-   속성의 정수 ID  
  
 속성 목록에 속성을 추가할 때 이름과 설명도 제공해야 합니다. 그러나 속성의 정식 이름과 설명을 사용할 필요는 없습니다.  
  
 이 항목에서는 사용 가능한 속성, 특히 Microsoft에서 정의한 속성에 대한 정보를 찾기 위해 일반적으로 사용되는 방법에 대해 설명합니다. 타사에서 정의한 속성에 대한 자세한 내용은 타사 설명서를 참조하거나 해당 공급업체에 문의하십시오.  
  
##  <a name="wellknown"></a> 널리 사용되고 잘 알려진 Microsoft 속성에 대한 정보 찾기  
 Microsoft에서는 여러 컨텍스트에서 사용할 수 있도록 수백 개의 문서 속성을 정의하지만 각 파일 형식에서는 사용 가능한 속성 중 일부만 사용합니다. 자주 사용되는 Windows 속성 중에는 작은 일반 속성 집합이 있습니다. 다음 표에서는 잘 알려진 일반 속성의 몇 가지 예를 보여 줍니다. 이 표에는 잘 알려진 이름, Windows 정식 이름(Microsoft에서 게시한 속성 설명에 포함됨), 속성 집합 GUID, 속성 정수 식별자 및 간단한 설명이 들어 있습니다.  
  
|잘 알려진 이름|Windows 정식 이름|속성 집합 GUID|정수 ID|설명|  
|----------------------|----------------------------|-----------------------|----------------|-----------------|  
|Authors|**System.Author**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|4|지정된 항목의 작성자입니다.|  
|Tags|**System.Keywords**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|5|항목에 할당된 키워드(태그라고도 함) 집합입니다.|  
|형식|**System.PerceivedType**|28636AA6-953D-11D2-B5D6-00C04FD918D0|9|정식 유형을 기반으로 인식되는 파일 유형입니다.|  
|Title|**System.Title**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|2|항목의 제목입니다. 예를 들어 문서의 제목, 메시지의 제목, 사진의 캡션 또는 음악 트랙의 이름이 여기에 해당합니다.|  
  
 파일 형식 간 일관성을 유지하기 위해 Microsoft에서는 몇 가지 문서 범주에 대해 자주 사용되고 우선 순위가 높은 문서 속성의 하위 집합을 식별했습니다. 여기에는 통신, 연락처, 문서, 음악 파일, 그림 및 동영상이 포함됩니다. 각 범주에서 순위가 높은 속성에 대한 자세한 내용은 Windows Search 설명서에서 [사용자 지정 파일 형식에 대한 시스템 정의 속성](https://go.microsoft.com/fwlink/?LinkId=144336) 을 참조하세요.  
  
 특정 파일 형식은 세 가지 유형의 속성을 구현할 수 있습니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서 정의한 일반 속성  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서 정의한 범주별 속성  
  
-   소프트웨어 공급업체에서 정의한 애플리케이션별 사용자 지정 속성  
  
##  <a name="filtdump"></a> FILTDUMP.EXE를 사용하여 사용 가능한 속성에 대한 정보 찾기  
 설치된 IFilter를 통해 검색되고 추출된 속성을 알아 보려면 **Windows SDK의 일부인** filtdump.exe [!INCLUDE[msCoName](../../includes/msconame-md.md)] 유틸리티를 설치하고 실행할 수 있습니다.  
  
 명령 프롬프트에서 **filtdump.exe** 를 실행하고 단일 인수를 제공합니다. 이 인수는 IFilter가 설치된 파일 형식을 사용하는 개별 파일의 이름입니다. 이 유틸리티는 문서에서 IFilter를 통해 검색된 모든 속성의 목록을 속성 집합 GUID, 정수 ID 및 추가 정보와 함께 표시합니다.  
  
 이 소프트웨어 설치에 대한 자세한 내용은 [Windows 7 및 .NET Framework 4용 Microsoft Windows SDK](https://www.microsoft.com/download/details.aspx?id=8279)를 참조하십시오. SDK를 다운로드하여 설치한 후 다음 폴더에서 filtdump.exe 유틸리티를 찾으십시오.  
  
-   64비트 버전의 경우 `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin\x64`을 찾아봅니다.  
  
-   32비트 버전의 경우 `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin`을 찾아봅니다.  
  
##  <a name="propdesc"></a> Windows 속성 설명에서 검색 속성 값 찾기  
 잘 알려진 Windows Search 속성의 경우 속성 설명( **propertyDescription** )의 **formatID** 및**propID**특성에서 필요한 정보를 가져올 수 있습니다.  
  
 다음 예에서는 일반적인 Microsoft 속성(이 경우 `System.Author` 속성) 설명의 관련 부분을 보여 줍니다. `formatID` 특성은 속성 집합 GUID로 `F29F85E0-4FF9-1068-AB91-08002B27B3D9`를 지정하고, `propID` 특성은 속성 정수 ID로 `4.` 를 지정합니다. `name` 특성은 Windows 정식 속성 이름으로 `System.Author`를 지정합니다. 이 예에서는 관련되지 않은 속성 설명의 부분을 생략합니다.  
  
```  
.  
propertyDescription  
name = System.Author  
...  
formatID = F29F85E0-4FF9-1068-AB91-08002B27B3D9  
propID = 4  
...  
```  
  
 이 속성의 전체 설명은 Windows 검색 설명서에서 [System.Author](https://go.microsoft.com/fwlink/?LinkId=144337) 를 참조하십시오.  
  
 Windows 속성의 전체 목록을 보려면 Windows 검색 설명서에서 [Windows 속성](https://go.microsoft.com/fwlink/?LinkId=215013)을 참조하십시오.  
  
##  <a name="examples"></a> 검색 속성 목록에 속성 추가  
 다음 예에서는 속성을 검색 속성 목록에 추가하는 방법을 보여 줍니다. 이 예에서는 [ALTER SEARCH PROPERTY LIST](../../t-sql/statements/alter-search-property-list-transact-sql.md) 문을 사용하여 `System.Author` 속성을 `PropertyList1`이라는 검색 속성 목록에 추가하고 속성에 `Author`라는 이름을 제공합니다.  
  
```  
ALTER SEARCH PROPERTY LIST PropertyList1   
  ADD 'Author'  
    WITH (  
          PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9',  
          PROPERTY_INT_ID = 4,   
          PROPERTY_DESCRIPTION = 'System.Author - the author or authors of the item'   
         )  
GO  
```  
  
 검색 속성 목록을 만들어 전체 텍스트 인덱스와 연결하는 방법은 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [검색 필터 구성 및 관리](../../relational-databases/search/configure-and-manage-filters-for-search.md)  
  
  
