---
title: SQL Server 이전 버전에서 네이티브 및 문자 형식 데이터 가져오기
description: SQL Server 2019에서는 bcp를 통해 -V 스위치와 한정자를 사용하여 다른 버전의 SQL Server에서 원시 형식 데이터와 문자 형식 데이터를 가져올 수 있습니다.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- earlier versions [SQL Server], import and export data formats
- -V switch
- data formats [SQL Server], earlier versions
- previous versions [SQL Server], import and export data formats
ms.assetid: e644696f-9017-428e-a5b3-d445d1c630b3
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 581888db5b930ce6f2b44a991e3ef1ef2f08525a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80980565"
---
# <a name="import-native-and-character-format-data-from-earlier-versions-of-sql-server"></a>SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 **bcp** 를 사용하면 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]-V [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]스위치를 통해 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , **또는** 에서 원시 및 문자 형식 데이터를 가져올 수 있습니다. **-V[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스위치를 사용하면** 에서 지정된 이전 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 데이터 형식이 사용되며, 데이터 파일 형식은 해당 이전 버전의 형식과 동일합니다.  
  
 데이터 파일에 대해 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 지정하려면 다음 한정자 중 하나와 함께 **-V** 스위치를 사용합니다.  
  
|SQL Server 버전|한정자|  
|------------------------|---------------|  
|[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]|**-V80**|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|**-V90**|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|**-V100**|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|**-V 110**|  
  
## <a name="interpretation-of-data-types"></a>데이터 형식 해석  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이후 버전에서는 몇 가지 새로운 형식을 지원합니다. 새 데이터 형식을 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전으로 가져오려면 이전 **bcp** 클라이언트에서 읽을 수 있는 형식으로 저장되어야 합니다. 다음 표에서는 새 데이터 형식을 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 호환되도록 변환하는 방법을 요약합니다.  
  
|SQL Server 2005의 새로운 데이터 형식|6*x*버전의 호환 데이터 형식|70 버전의 호환 데이터 형식|80 버전의 호환 데이터 형식|  
|---------------------------------------|-------------------------------------------|-----------------------------------------|-----------------------------------------|  
|**bigint**|**decimal**|**decimal**|*|  
|**sql_variant**|**text**|**nvarchar(4000)**|*|  
|**varchar(max)**|**text**|**text**|**text**|  
|**nvarchar(max)**|**ntext**|**ntext**|**ntext**|  
|**varbinary(max)**|**image**|**image**|**image**|  
|XML|**ntext**|**ntext**|**ntext**|  
|UDT**|**image**|**image**|**image**|  
  
 *이 형식은 기본적으로 지원됩니다.  
  
 **UDT는 사용자 정의 형식을 나타냅니다.  
  
## <a name="exporting-using--v-80"></a>–V 80을 사용하여 내보내기  
 **–V80** 스위치를 사용하여 데이터를 대량으로 내보내는 경우 기본 모드의 **nvarchar(max)** , **varchar(max)** , **varbinary(max)** , XML 및 UDT 데이터는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전의 기본값인 8바이트 접두사가 아니라 **text**, **image** 및 **ntext** 데이터와 같은 4바이트 접두사를 사용하여 저장됩니다.  
  
## <a name="copying-date-values"></a>날짜 값 복사  
 **bcp** 는 ODBC 대량 복사 API를 사용합니다. 따라서 데이터 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 가져오기 위해 **bcp** 는 ODBC 날짜 형식(*yyyy-mm-dd hh:mm:ss*[ *.f...* ])을 사용합니다.  
  
 **bcp** 명령은 **datetime** 및 **smalldatetime** 값에 대해 ODBC 기본 형식을 사용하여 문자 형식 데이터 파일을 내보냅니다. 예를 들어 **이라는 날짜가 포함된** datetime `12 Aug 1998` 열은 `1998-08-12 00:00:00.000`문자열로 데이터 파일에 대량 복사됩니다.  
  
> [!IMPORTANT]  
>  **bcp** 를 사용하여 **smalldatetime**필드로 데이터를 가져올 때 초 값이 00.000인지 확인하세요. 그렇지 않으면 작업이 실패합니다. **smalldatetime** 데이터 형식은 가장 근접한 분 값만 갖습니다. 이 경우 BULK INSERT 및 INSERT ... SELECT * FROM OPENROWSET(BULK...)는 이 경우 실패하지 않지만 초 값이 잘립니다.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
 **대량 가져오기 또는 대량 내보내기를 위한 데이터 형식을 사용하려면**  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [SQL Server 데이터베이스 엔진의 이전 버전과의 호환성](../../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
