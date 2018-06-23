---
title: 대량 가져오기 수행 중 Null 유지 또는 기본값 사용(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- bulk importing [SQL Server], null values
- bulk importing [SQL Server], default values
- data formats [SQL Server], null values
- bulk rowset providers [SQL Server]
- bcp utility [SQL Server], null values
- BULK INSERT statement
- default values
- OPENROWSET function, bulk importing
- data formats [SQL Server], default values
ms.assetid: 6b91d762-337b-4345-a159-88abb3e64a81
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7840877066f5f941050d96c3274ab7bf6698326c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184706"
---
# <a name="keep-nulls-or-use-default-values-during-bulk-import-sql-server"></a>대량 가져오기 수행 중 Null 유지 또는 기본값 사용(SQL Server)
  기본적으로 데이터를 테이블로 가져올 때 **bcp** 명령 및 BULK INSERT 문은 해당 테이블의 열에 대해 정의된 기본값을 유지합니다. 예를 들어 데이터 파일에 null 필드가 있으면 열의 기본값이 대신 로드됩니다. **bcp** 명령 및 BULK INSERT 문을 사용하면 Null 값을 유지하도록 지정할 수 있습니다.  
  
 반대로 일반 INSERT 문은 기본값을 삽입하는 대신 Null 값을 유지합니다. INSERT ... SELECT * FROM OPENROWSET(BULK...) 문은 일반 INSERT와 같은 기본 동작을 제공하지만 기본값 삽입에 대한 테이블 힌트를 추가로 지원합니다.  
  
> [!NOTE]  
>  테이블 열 건너뛰기 예제 서식 파일은 [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)를 참조하세요.  
  
## <a name="sample-table-and-data-file"></a>예제 테이블 및 데이터 파일  
 이 항목의 예를 실행하려면 예제 테이블 및 데이터 파일을 만들어야 합니다.  
  
### <a name="sample-table"></a>예제 테이블  
 이 예에서는 **dbo** 스키마의 **AdventureWorks** 예제 데이터베이스에서 **MyTestDefaultCol2** 라는 이름의 테이블을 만들어야 합니다. 이 테이블을 만들려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음을 실행합니다.  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE MyTestDefaultCol2   
(Col1 smallint,  
Col2 nvarchar(50) DEFAULT 'Default value of Col2',  
Col3 nvarchar(50)   
);  
GO  
  
```  
  
 두 번째 테이블 열 `Col2`는 기본값을 가집니다.  
  
### <a name="sample-format-file"></a>예제 서식 파일  
 일부 대량 가져오기 예에서는 XML이 아닌 서식 파일(`MyTestDefaultCol2-f-c.Fmt`)을 사용하는데 이 파일은 `MyTestDefaultCol2` 테이블과 정확히 일치합니다. 이 서식 파일을 만들려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
bcp AdventureWorks..MyTestDefaultCol2 format nul -c -f C:\MyTestDefaultCol2-f-c.Fmt -t, -r\n -T  
  
```  
  
 서식 파일을 만드는 방법은 [서식 파일 만들기&#40;SQL Server&#41;](create-a-format-file-sql-server.md)를 참조하세요.  
  
### <a name="sample-data-file"></a>예제 데이터 파일  
 이 예에서는 예제 데이터 파일( `MyTestEmptyField2-c.Dat`)을 사용하는데 이 파일은 두 번째 필드에 값이 없습니다. `MyTestEmptyField2-c.Dat` 데이터 파일에는 다음 레코드가 포함됩니다.  
  
```  
1,,DataField3  
2,,DataField3  
  
```  
  
## <a name="keeping-null-values-with-bcp-or-bulk-insert"></a>bcp 또는 BULK INSERT로 Null 값 유지  
 다음 한정자는 대량 가져오기 작업 중 테이블 열에 대한 기본값(있는 경우)을 상속하기보다는 데이터 파일의 빈 필드에 Null 값을 유지하도록 지정합니다.  
  
|Command|한정자|한정자 유형|  
|-------------|---------------|--------------------|  
|**bcp**|`-k`|스위치|  
|BULK INSERT|KEEPNULLS<sup>1</sup>|인수|  
  
 <sup>1</sup> 대량 삽입에 대 한 기본값을 사용할 수 없는 경우는 테이블 열 정의 해야 null 값을 허용 하도록 합니다.  
  
> [!NOTE]  
>  이러한 한정자는 대량 가져오기 명령을 통해 테이블에서 DEFAULT 정의 확인을 비활성화합니다. 그러나 동시 INSERT 문의 경우 DEFAULT 정의가 있어야 합니다.  
  
 자세한 내용은 [bcp 유틸리티](../../tools/bcp-utility.md) 및 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)를 참조하세요.  
  
### <a name="examples"></a>예  
 이 섹션의 예에서는 **bcp** 또는 BULK INSERT를 사용하여 대량 가져오기를 수행하고 Null 값을 유지합니다.  
  
 두 번째 테이블 열 **Col2**는 기본값을 가집니다. 데이터 파일의 해당되는 필드에는 빈 문자열이 포함됩니다. 기본적으로 **bcp** 또는 BULK INSERT를 사용하여 이 데이터 파일에서 **MyTestDefaultCol2** 테이블로 데이터를 가져오면 **Col2** 의 기본값이 삽입되어 다음과 같은 결과가 생성됩니다.  
  
||||  
|-|-|-|  
|`1`|`Default value of Col2`|`DataField3`|  
|`2`|`Default value of Col2`|`DataField3`|  
  
 삽입할 "`NULL`instead of`Default value of Col2`"를 사용 해야는 `-k` 스위치 또는 KEEPNULL 옵션을 다음에 표시 된 대로 **bcp** 및 BULK INSERT 예입니다.  
  
#### <a name="using-bcp-and-keeping-null-values"></a>bcp 사용 및 Null 값 유지  
 다음 예에서는 **bcp** 명령에서 Null 값을 유지하는 방법을 설명합니다. **bcp** 명령에는 다음 스위치가 포함됩니다.  
  
|스위치|Description|  
|------------|-----------------|  
|`-f`|해당 명령에서 서식 파일을 사용하도록 지정합니다.|  
|`-k`|작업 시 삽입된 열에 기본값이 지정되지 않고 빈 열이 Null 값을 보유하도록 지정합니다.|  
|`-T`|bcp 유틸리티가 트러스트된 연결을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 연결되도록 지정합니다.|  
  
 Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
bcp AdventureWorks..MyTestDefaultCol2 in C:\MyTestEmptyField2-c.Dat -f C:\MyTestDefaultCol2-f-c.Fmt -k -T  
  
```  
  
#### <a name="using-bulk-insert-and-keeping-null-values"></a>BULK INSERT 사용 및 Null 값 유지  
 다음 예에서는 BULK INSERT 문에서 KEEPNULLS 옵션을 사용하는 방법을 보여 줍니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 쿼리 편집기 같은 쿼리 도구에서 다음을 실행합니다.  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT MyTestDefaultCol2  
   FROM 'C:\MyTestEmptyField2-c.Dat'  
   WITH (  
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ',',  
      KEEPNULLS  
   );  
GO  
  
```  
  
## <a name="keeping-default-values-with-insert--select--from-openrowsetbulk"></a>INSERT ... 로 기본 값 사용  
 기본적으로 대량 로드 작업에 지정되어 있지 않은 열은 INSERT ... SELECT * FROM OPENROWSET(BULK...)을 사용하여 네이티브 형식 데이터를 테이블로 가져올 수 있습니다. 그러나 데이터 파일의 빈 필드의 경우 해당 테이블 열에서 기본값(있는 경우)을 사용하도록 지정할 수 있습니다. 기본값을 사용하려면 다음 테이블 힌트를 지정하십시오.  
  
|Command|한정자|한정자 유형|  
|-------------|---------------|--------------------|  
|INSERT ... 로 기본 값 사용|WITH(KEEPDEFAULTS)|테이블 힌트|  
  
> [!NOTE]  
>  자세한 내용은 [INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql), [SELECT&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql), [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql) 및 [테이블 힌트&#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)를 참조하세요.  
  
### <a name="examples"></a>예  
 다음 INSERT ... SELECT * FROM OPENROWSET(BULK...) 예는 데이터를 대량으로 가져오고 기본값을 유지합니다.  
  
 이 예를 실행하려면 **MyTestDefaultCol2** 예제 테이블과 `MyTestEmptyField2-c.Dat` 데이터 파일을 만들고 `MyTestDefaultCol2-f-c.Fmt`서식 파일을 사용해야 합니다. 이러한 예제를 만드는 방법은 이 항목의 앞 부분에 있는 "예제 테이블 및 데이터 파일"을 참조하십시오.  
  
 두 번째 테이블 열 **Col2**는 기본값을 가집니다. 데이터 파일의 해당되는 필드에는 빈 문자열이 포함됩니다. INSERT ... SELECT \* FROM OPENROWSET(BULK...)가 이 데이터 파일의 필드를 **MyTestDefaultCol2** 테이블로 가져올 때 기본적으로 기본값 대신 NULL이 **Col2**로 삽입됩니다. 이 기본 동작을 통해 다음과 같은 결과가 나타납니다.  
  
||||  
|-|-|-|  
|`1`|`NULL`|`DataField3`|  
|`2`|`NULL`|`DataField3`|  
  
 "`Default value of Col2`" 대신 기본값인 "`NULL`" 를 삽입하려면 다음 예에서 예시하는 대로 KEEPDEFAULTS 테이블 힌트를 사용해야 합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 쿼리 편집기 같은 쿼리 도구에서 다음을 실행합니다.  
  
```  
USE AdventureWorks;  
GO  
INSERT INTO MyTestDefaultCol2  
    WITH (KEEPDEFAULTS)  
    SELECT *  
      FROM OPENROWSET(BULK  'C:\MyTestEmptyField2-c.Dat',  
      FORMATFILE='C:\MyTestDefaultCol2-f-c.Fmt'       
      ) as t1 ;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [데이터 대량 가져오기 중 ID 값 유지&#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [대량 내보내기 또는 가져오기를 위한 데이터 준비&#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **서식 파일을 사용하려면**  
  
-   [서식 파일 만들기&#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **대량 가져오기 또는 대량 내보내기를 위한 데이터 형식을 사용하려면**  
  
-   [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [네이티브 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **bcp를 사용할 때 데이터 형식의 호환 가능성을 지정하려면**  
  
-   [필드 및 행 종결자 지정&#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
-   [bcp를 사용하여 데이터 파일에 접두사 길이 지정&#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [bcp를 사용하여 파일 저장 유형 지정&#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [테이블 힌트&#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)  
  
  
