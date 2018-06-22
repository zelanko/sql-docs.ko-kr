---
title: OLE DB 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 13a82d41-dd7a-4708-bc84-4407a536c877
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a4c29542fe95e7f7323ac7d8975f391ba97ea274
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089973"
---
# <a name="ole-db-custom-properties"></a>OLE DB 사용자 지정 속성
  **원본 사용자 지정 속성**  
  
 OLE DB 원본에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 OLE DB 원본의 사용자 지정 속성에 대해 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|정수|데이터베이스에 액세스하는 데 사용되는 모드입니다. 가능한 값은 **행 집합 열기**, **변수에서 행 집합 열기**, `SQL Command`, 및 **변수를 사용한 SQL 명령**합니다. 기본값은 **행 집합 열기**입니다.|  
|AlwaysUseDefaultCodePage|Boolean|값을 사용할지 여부를 나타내는 값은 `DefaultCodePage` 속성 각 열에 대해 아니면 각 열의 로캘에서 코드 페이지를 파생 하려고 합니다. 이 속성의 기본값은 `False`합니다.|  
|CommandTimeout|정수|명령이 종료되기 전의 제한 시간(초)입니다. 값 0은 제한 시간이 없음을 나타냅니다.<br /><br /> 참고: 이 속성은 **OLE DB 원본 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|DefaultCodePage|정수|데이터 원본에서 코드 페이지 정보를 사용할 수 없을 경우 사용할 코드 페이지입니다.|  
|OpenRowset|String|행 집합을 여는 데 사용되는 데이터베이스 개체의 이름입니다.|  
|OpenRowsetVariable|String|행 집합을 여는 데 사용되는 데이터베이스 개체의 이름이 포함된 변수입니다.|  
|ParameterMapping|String|SQL 명령의 매개 변수에서 변수로의 매핑입니다.|  
|SqlCommand|String|실행할 SQL 명령입니다.|  
|SqlCommandVariable|String|실행할 SQL 명령이 포함된 변수입니다.|  
  
 OLE DB 원본의 출력 및 출력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [OLE DB Source](ole-db-source.md)을(를) 참조하세요.  
  
 **대상 사용자 지정 속성**  
  
 OLE DB 대상에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 OLE DB 대상의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
> [!NOTE]  
>  표시 하는 이름이 비슷한 속성에 해당 하는 위에 나열 된 FastLoad 옵션 (FastLoadKeepIdentity, FastLoadKeepNulls 및 FastLoadOptions)은 `IRowsetFastLoad` SQL Server (SQLOLEDB)에 대 한 Microsoft OLE DB Provider에서 구현 된 인터페이스입니다. 자세한 내용을 보려면 MSDN Library에서 IRowsetFastLoad를 검색하십시오.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer(열거형)|대상에서 해당하는 대상 데이터베이스에 액세스하는 방법을 지정하는 값입니다.<br /><br /> 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> `OpenRowset` (0): 테이블 또는 뷰의 이름을 제공 해야 합니다.<br />`OpenRowset from Variable` (1): 테이블 또는 뷰의 이름이 포함 된 변수의 이름을 제공 해야 합니다.<br />`OpenRowset Using Fastload` (3): 테이블 또는 뷰의 이름을 제공 해야 합니다.<br />`OpenRowset Using Fastload from Variable` (4): 테이블 또는 뷰의 이름이 포함 된 변수의 이름을 제공 해야 합니다.<br />`SQL Command` (2): SQL 문을 제공 해야 합니다.|  
|AlwaysUseDefaultCodePage|Boolean|값을 사용할지 여부를 나타내는 값은 `DefaultCodePage` 속성 각 열에 대해 아니면 각 열의 로캘에서 코드 페이지를 파생 하려고 합니다. 이 속성의 기본값은 `False`합니다.|  
|CommandTimeout|정수|제한 시간이 초과될 때까지 SQL 명령을 실행할 수 있는 최대 시간(초)입니다. 값 0은 제한 시간이 없음을 의미합니다. 이 속성의 기본값은 0입니다.<br /><br /> 참고: 이 속성은 **OLE DB 대상 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|DefaultCodePage|정수|OLE DB 대상과 연결되는 기본 코드 페이지입니다.|  
|FastLoadKeepIdentity|Boolean|데이터를 로드할 때 ID 값을 복사할지 여부를 지정하는 값입니다. 이 속성은 빠른 로드 옵션 중 하나와 함께 사용해야 합니다. 이 속성의 기본값은 `False`합니다. 이 속성은 OLE DB에 해당 [IRowsetFastLoad &#40;OLE DB&#41; ](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) 속성 `SSPROP_FASTLOADKEEPIDENTITY`합니다.|  
|FastLoadKeepNulls|Boolean|데이터를 로드할 때 Null 값을 복사할지 여부를 지정하는 값입니다. 이 속성은 빠른 로드 옵션 중 하나와 함께 사용해야 합니다. 이 속성의 기본값은 `False`합니다. 이 속성은 OLE DB에 해당 [IRowsetFastLoad &#40;OLE DB&#41; ](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) 속성 `SSPROP_FASTLOADKEEPNULLS`합니다.|  
|FastLoadMaxInsertCommitSize|정수|OLE DB 대상에서 빠른 로드 작업을 수행하는 동안 커밋을 시도하는 일괄 처리 크기를 지정하는 값입니다. 기본값인 **0**은 모든 행이 처리된 후의 단일 커밋 작업을 나타냅니다.|  
|FastLoadOptions|String|빠른 로드 옵션 모음입니다. 빠른 로드 옵션에는 테이블 잠금 및 제약 조건 검사가 포함됩니다. 둘 다 또는 둘 중 하나를 지정하거나 아무 것도 지정하지 않을 수 있습니다. 이 속성은 OLE DB IRowsetFastLoad 속성에 해당 `SSPROP_FASTLOADOPTIONS` 와 같은 문자열 옵션을 허용 하 고 `CHECK_CONSTRAINTS` 및 `TABLOCK`합니다.<br /><br /> 참고: 이 속성의 일부 옵션은 **Excel 대상 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|OpenRowset|String|AccessMode 다음과 같은 경우 `OpenRowset`, OLE DB 대상에서 액세스 하는 뷰나 테이블의 이름입니다.|  
|OpenRowsetVariable|String|AccessMode 다음과 같은 경우 `OpenRowset from Variable`, OLE DB 대상에서 액세스 하는 뷰나 테이블의 이름이 포함 된 변수의 이름입니다.|  
|SqlCommand|String|AccessMode 다음과 같은 경우 `SQL Command`, OLE DB 대상을 사용 하 여 데이터에 대 한 대상 열을 지정 하는 Transact SQL 문입니다.|  
  
 OLE DB 대상의 입력 및 입력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [OLE DB Destination](ole-db-destination.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Common Properties](../common-properties.md)  
  
  