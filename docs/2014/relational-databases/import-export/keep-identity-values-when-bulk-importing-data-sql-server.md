---
title: 데이터 대량 가져오기 중 ID 값 유지(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- identity values [SQL Server], bulk imports
- data formats [SQL Server], identity values
- bulk importing [SQL Server], identity values
ms.assetid: 45894a3f-2d8a-4edd-9568-afa7d0d3061f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5bb2fbd3129475c5d712cd4d1fce8bbe29ea096f
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011913"
---
# <a name="keep-identity-values-when-bulk-importing-data-sql-server"></a>데이터 대량 가져오기 중 ID 값 유지(SQL Server)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 ID 값이 들어 있는 데이터 파일을 대량으로 가져옵니다. 기본적으로 가져온 데이터 파일의 ID 열 값은 무시되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 자동으로 고유 값을 할당합니다. 고유 값은 테이블 작성 중에 지정된 초기 및 증분 값을 기준으로 합니다.  
  
 데이터 파일에 테이블의 ID 열에 대한 값이 없으면 서식 파일을 사용하여 데이터를 가져올 때 테이블의 ID 열을 건너뛰어야 함을 지정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 자동으로 열에 고유 값을 할당합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 ID 값을 할당하지 않으면서 테이블에 데이터 행을 대량으로 가져오려면 적절한 ID 유지 명령 한정자를 사용합니다. ID 유지 한정자를 지정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 데이터 파일의 ID 값을 사용합니다. 이러한 한정자는 다음과 같습니다.  
  
|Command|ID 유지 한정자|한정자 유형|  
|-------------|------------------------------|--------------------|  
|`bcp`|**-E**|스위치|  
|BULK INSERT|KEEPIDENTITY|인수|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|KEEPIDENTITY|테이블 힌트|  
  
 자세한 내용은 [bcp 유틸리티](../../tools/bcp-utility.md), [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql), [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql), [INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql), [SELECT&#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql) 및 [테이블 힌트&#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)를 참조하세요.  
  
> [!NOTE]  
>  여러 테이블에서 사용할 수 있거나 테이블을 참조하지 않고 애플리케이션에서 호출할 수 있는 자동으로 증가하는 번호를 만들려면 [시퀀스 번호](../sequence-numbers/sequence-numbers.md)를 참조하세요.  
  
## <a name="examples"></a>예  
 이 항목의 예에서는 INSERT ... SELECT * FROM OPENROWSET(BULK...)을 사용하고 기본값을 유지하여 데이터를 대량으로 가져옵니다.  
  
### <a name="sample-table"></a>예제 테이블  
 대량 가져오기 예제에서는 **dbo** 스키마의 **AdventureWorks** 샘플 데이터베이스에 **myTestKeepNulls** 테이블을 만들어야 합니다. 이 테이블을 만들려면 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음을 실행합니다.  
  
```  
USE AdventureWorks;  
GO  
SELECT * INTO HumanResources.myDepartment   
   FROM HumanResources.Department  
      WHERE 1=0;  
GO  
SELECT * FROM HumanResources.myDepartment;  
```  
  
 `myDepartment`의 기반이 되는 **Department** 테이블은 IDENTITY_INSERT가 OFF로 설정되어 있습니다. 따라서 ID 열로 데이터를 가져오려면 KEEPIDENTITY 또는 **-E**를 지정해야 합니다.  
  
### <a name="sample-data-file"></a>예제 데이터 파일  
 대량 가져오기 예에 사용된 데이터 파일에는 `HumanResources.Department` 테이블에서 네이티브 형식으로, 대량으로 내보낸 데이터가 들어 있습니다. 데이터 파일을 만들려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
bcp AdventureWorks.HumanResources.Department out myDepartment-n.Dat -n -T  
```  
  
### <a name="sample-format-file"></a>예제 서식 파일  
 이 대량 가져오기 예에서는 네이티브 데이터 형식을 사용하는 XML 서식 파일인 `myDepartment-f-x-n.Xml`을 사용합니다. 이 예에서는 `bcp`를 사용하여 `HumanResources.Department` 데이터베이스의 `AdventureWorks` 테이블에서 이 서식 파일을 만듭니다. Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
bcp AdventureWorks.HumanResources.Department format nul -n -x -f myDepartment-f-n-x.Xml -T  
```  
  
 서식 파일을 만드는 방법은 [서식 파일 만들기&#40;SQL Server&#41;](create-a-format-file-sql-server.md)를 참조하세요.  
  
### <a name="a-using-bcp-and-keeping-identity-values"></a>1. bcp 사용 및 ID 값 유지  
 다음 예에서는 `bcp`를 사용하여 데이터를 대량으로 가져올 때 ID 값을 유지하는 방법을 보여 줍니다. `bcp` 명령은 서식 파일인 `myDepartment-f-n-x.Xml`을 사용하며 다음 스위치를 포함합니다.  
  
|한정자|Description|  
|----------------|-----------------|  
|**-E**|데이터 파일의 ID 값이 ID 열에 사용되도록 지정합니다.|  
|**-T**|지정 된 `bcp` 유틸리티에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 트러스트 된 연결 사용 합니다.|  
  
 Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
bcp AdventureWorks.HumanResources.myDepartment in C:\myDepartment-n.Dat -f C:\myDepartment-f-n-x.Xml -E -T  
  
```  
  
### <a name="b-using-bulk-insert-and-keeping-identity-values"></a>2. BULK INSERT 사용 및 ID 값 유지  
 다음 예에서는 BULK INSERT를 사용하여 `myDepartment-c.Dat` 데이터 파일에서 `AdventureWorks.HumanResources.myDepartment` 테이블로 데이터를 대량으로 가져옵니다. 해당 문은 `myDepartment-f-n-x.Xml` 서식 파일을 사용하며 KEEPIDENTITY 옵션을 포함하여 데이터 파일의 모든 ID를 유지합니다.  
  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음을 실행합니다.  
  
```  
USE AdventureWorks;  
GO  
DELETE HumanResources.myDepartment;  
GO  
BULK INSERT HumanResources.myDepartment  
   FROM 'C:\myDepartment-n.Dat'  
   WITH (  
      KEEPIDENTITY,  
      FORMATFILE='C:\myDepartment-f-n-x.Xml'  
   );  
GO  
SELECT * FROM HumanResources.myDepartment;  
  
```  
  
### <a name="c-using-openrowset-and-keeping-identity-values"></a>3. OPENROWSET 사용 및 ID 값 유지  
 다음 예에서는 OPENROWSET 대량 행 집합 공급자를 사용하여 `myDepartment-c.Dat` 파일에서 `AdventureWorks.HumanResources.myDepartment` 테이블로 데이터를 대량으로 가져옵니다. 해당 문은 `myDepartment-f-n-x.Xml` 서식 파일을 사용하고 KEEPIDENTITY 힌트를 포함하여 데이터 파일의 모든 ID 값을 유지합니다.  
  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음을 실행합니다.  
  
```  
USE AdventureWorks;  
GO  
DELETE HumanResources.myDepartment;  
GO  
  
INSERT INTO HumanResources.myDepartment  
   with (KEEPIDENTITY)  
   (DepartmentID, Name, GroupName, ModifiedDate)  
   SELECT *  
      FROM  OPENROWSET(BULK 'C:\myDepartment-n.Dat',  
      FORMATFILE='C:\myDepartment-f-n-x.Xml') as t1;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
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
  
1.  [필드 및 행 종결자 지정&#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
2.  [bcp를 사용하여 데이터 파일에 접두사 길이 지정&#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [bcp를 사용하여 파일 저장 유형 지정&#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [테이블 힌트&#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)  
  
  
