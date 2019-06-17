---
title: 데이터를 가져오거나 내보내기 위해 유니코드 네이티브 형식 사용(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- Unicode [SQL Server], bulk importing and exporting
- data formats [SQL Server], Unicode native
ms.assetid: a6213308-f3d5-406e-9029-19d8bb3367f3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b1d115dacc53cb074080931c2ebad88dcaf1c68d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011571"
---
# <a name="use-unicode-native-format-to-import-or-export-data-sql-server"></a>데이터를 가져오거나 내보내기 위해 유니코드 네이티브 형식 사용(SQL Server)
  유니코드 네이티브 형식은 한 곳의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에서 다른 설치로 정보를 복사해야 하는 경우 유용합니다. 비문자 형식의 데이터에 네이티브 형식을 사용하면 문자 형식과 다른 데이터 형식 간의 불필요한 변환을 막고 시간을 절약할 수 있습니다. 모든 문자 형식의 데이터에 유니코드 문자 형식을 사용하면 다른 코드 페이지를 사용하는 서버 간에 데이터를 대량 로드할 때 확장 문자의 손실을 방지할 수 있습니다. 유니코드 네이티브 형식의 데이터 파일은 어떤 대량 가져오기 방법으로도 읽을 수 있습니다.  
  
 확장 또는 DBCS 문자를 포함하는 데이터 파일을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 여러 인스턴트 사이에 대량의 데이터를 전송하는 경우 유니코드 네이티브 형식을 사용하는 것이 좋습니다. 비문자 데이터의 경우 유니코드 네이티브 형식은 네이티브(데이터베이스) 데이터 형식을 사용합니다. `char`, `nchar`, `varchar`, `nvarchar`, `text`, `varchar(max)`, `nvarchar(max)` 및 `ntext`와 같은 문자 데이터의 경우 유니코드 네이티브 형식은 유니코드 문자 데이터 형식을 사용합니다.  
  
 유니코드 네이티브 형식의 데이터 파일에 SQLVARIANT로 저장된 `sql_variant` 데이터는 `char` 및 `varchar` 값이 `nchar` 및 `nvarchar`로 변환되어 영향을 받은 열에 두 배의 저장 공간이 필요하다는 점을 제외하고 네이티브 형식의 데이터 파일과 같은 방법으로 작동합니다. 테이블 열로 대량 가져오기를 수행하면 원래의 메타데이터는 유지되고 값은 원래의 `char` 및 `varchar` 데이터 형식으로 다시 변환됩니다.  
  
## <a name="command-options-for-unicode-native-format"></a>유니코드 네이티브 형식의 명령 옵션  
 **bcp**, BULK INSERT 또는 INSERT ... SELECT \* FROM OPENROWSET(BULK...)를 사용하여 테이블로 유니코드 원시 형식 데이터를 가져올 수 있습니다. **bcp** 명령 또는 BULK INSERT 문의 경우 명령줄에서 데이터 형식을 지정할 수 있습니다. INSERT ... SELECT * FROM OPENROWSET(BULK...) 문의 경우 서식 파일에서 데이터 형식을 지정해야 합니다.  
  
 다음 옵션으로 유니코드 네이티브 형식을 사용할 수 있습니다.  
  
|Command|옵션|Description|  
|-------------|------------|-----------------|  
|**bcp**|**-N**|발생 합니다 **bcp** 유틸리티가 네이티브 (데이터베이스) 데이터를 사용 하는 유니코드 네이티브 형식으로 사용 하도록 모든 비문자 데이터 및 모든 문자에 대 한 유니코드 문자 데이터 형식에 대 한 형식 (`char`, `nchar`, `varchar`, `nvarchar`하십시오 `text`, 및 `ntext`) 데이터.|  
|BULK INSERT|DATAFILETYPE **='** widenative **'**|데이터를 대량으로 가져올 때 유니코드 네이티브 형식을 사용합니다.|  
  
 자세한 내용은 [bcp 유틸리티](../../tools/bcp-utility.md), [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) 또는 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)를 참조하세요.  
  
> [!NOTE]  
>  서식 파일에서 필드 단위로 서식을 지정할 수도 있습니다. 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 **bcp** 를 사용하여 네이티브 데이터의 대량 내보내기를 수행하고 내보낸 데이터에 BULK INSERT를 사용하여 대량 가져오기를 수행하는 방법을 보여 줍니다.  
  
### <a name="sample-table"></a>예제 테이블  
 이 예에서는 **dbo** 스키마의 **AdventureWorks** 예제 데이터베이스에 **myTestUniNativeData** 라는 테이블이 필요하며 예를 실행하려면 이 테이블을 만들어야 합니다. [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음을 실행합니다.  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestUniNativeData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 이 테이블을 채우고 결과 내용을 확인하려면 다음 문을 실행합니다.  
  
```  
INSERT INTO myTestUniNativeData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestUniNativeData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestUniNativeData  
  
```  
  
### <a name="using-bcp-to-bulk-export-native-data"></a>bcp를 사용하여 네이티브 데이터 대량 내보내기  
 테이블의 데이터를 데이터 파일로 내보내려면 **out** 옵션 및 다음 한정자가 있는 **bcp** 를 사용합니다.  
  
|한정자|Description|  
|----------------|-----------------|  
|**-N**|네이티브 데이터 형식을 지정합니다.|  
|**-T**|**bcp** 유틸리티가 통합 보안을 사용하는 트러스트된 연결을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 연결되도록 지정합니다. **-T** 를 지정하지 않은 경우 성공적으로 로그인하려면 **-U** 와 **-P** 를 지정해야 합니다.|  
  
 다음 예에서는 `myTestUniNativeData` 테이블에서 `myTestUniNativeData-N.Dat` 데이터 파일로 네이티브 형식의 데이터를 대량으로 내보냅니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 명령 프롬프트에 다음을 입력합니다.  
  
```  
bcp AdventureWorks..myTestUniNativeData out C:\myTestUniNativeData-N.Dat -N -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-native-data"></a>BULK INSERT를 사용하여 네이티브 데이터 대량 가져오기  
 다음 예에서는 BULK INSERT를 사용하여 `myTestUniNativeData-N.Dat` 데이터 파일의 데이터를 `myTestUniNativeData` 테이블로 가져옵니다. [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음을 실행합니다.  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestUniNativeData   
    FROM 'C:\myTestUniNativeData-N.Dat'   
   WITH (DATAFILETYPE='widenative');   
GO  
SELECT Col1,Col2,Col3 FROM myTestUniNativeData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **대량 가져오기 또는 대량 내보내기를 위한 데이터 형식을 사용하려면**  
  
-   [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [네이티브 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [데이터 형식&#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)  
  
  
