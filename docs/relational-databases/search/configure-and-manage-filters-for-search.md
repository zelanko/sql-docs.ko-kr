---
description: 검색 필터 구성 및 관리
title: 검색 필터 구성 및 관리 | Microsoft 문서
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], filters
- filters [full-text search]
ms.assetid: 7ccf2ee0-9854-4253-8cca-1faed43b7095
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3cb9d2938bddb44f22f4429daf0de0705ea53b65
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460126"
---
# <a name="configure-and-manage-filters-for-search"></a>검색 필터 구성 및 관리
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  **varbinary**, **varbinary(max)**, **image** 또는 **xml** 데이터 형식 열의 문서를 인덱싱하려면 추가 처리가 필요합니다. 이러한 처리를 수행하려면 필터를 사용해야 합니다. 필터는 문서에서 서식이 제거된 텍스트 정보를 추출합니다. 그런 다음 필터는 테이블 열과 연결된 언어의 단어 분리기 구성 요소에 텍스트를 보냅니다.  
 
## <a name="filters-and-document-types"></a>필터 및 문서 유형
지정된 필터는 지정된 문서 유형(.doc, .pdf, .xls, .xml 등)에만 해당됩니다. 이러한 필터는 IFilter 인터페이스를 구현합니다. 이러한 문서 유형에 대한 자세한 내용을 보려면 [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md) 카탈로그 뷰를 쿼리하세요.  
  
이진 문서는 단일 **varbinary(max)** 또는 **image** 열에 저장할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 각 문서에 대해 파일 확장명을 기준으로 사용할 필터를 정확히 선택합니다. **varbinary(max)** 또는 **image** 열에 파일을 저장할 때는 파일 확장명을 볼 수 없으므로 별도의 테이블 열, 즉 유형 열에 따로 파일 확장명(.doc, .xls, .pdf 등)을 저장해야 합니다. 이 형식 열은 모든 문자 기반 데이터 형식이 될 수 있고 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word 문서를 나타내는 .doc와 같은 문서 파일 확장명을 포함합니다. **의** Document [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]테이블에서 **Document** 열은 **varbinary(max)** 형식이고 **FileExtension** 유형 열은 **nvarchar(8)** 형식입니다.  

**기존 전체 텍스트 인덱스의 유형 열을 보려면**  
  
-   [sys.fulltext_index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
  
> [!NOTE]  
>  필터 구현에 따라 필터에서 부모 개체에 포함된 개체를 처리할 수도 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 다른 개체에 대한 링크를 따라가도록 필터를 구성하지 않습니다.  

## <a name="installed-filters"></a>설치된 필터 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 고유한 XML 및 HTML 필터를 설치합니다. 또한 운영 체제에 설치되어 있는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 소유 형식(.doc, .xdoc, .ppt 등)용 필터도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 로드합니다. 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 로드되어 있는 필터를 확인하려면 [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md) 저장 프로시저를 다음과 같이 사용합니다.  

```sql
EXEC sp_help_fulltext_system_components 'filter';   
```  

> [!NOTE]
> .xlsx 지원을 제공하는 Office Filter Pack의 최신 버전을 사용하더라도 SQL Server는 엄격한 Open XML 스프레드시트를 지원하지 않습니다.  오류가 반환되지 않고 SQL Server는 엄격한 Open XML 스프레드시트 내용을 인덱싱하지 못합니다.

## <a name="non-microsoft-filters"></a>타사 필터
하지만 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 형식 이외의 다른 형식용 필터를 사용하려면 수동으로 서버 인스턴스에 로드해야 합니다. 추가 필터 설치에 대한 자세한 내용은 [등록된 필터와 단어 분리기 보기 및 변경](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)을 참조하세요.  
  
  
## <a name="see-also"></a>참고 항목  
 [sys.fulltext_index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [FILESTREAM과 기타 SQL Server 기능 간 호환성](../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)  
  
  
