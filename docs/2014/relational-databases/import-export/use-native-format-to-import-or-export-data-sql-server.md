---
title: 네이티브 형식을 사용하여 데이터 가져오기 및 내보내기(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- native data format [SQL Server]
- data formats [SQL Server], native
ms.assetid: eb279b2f-0f1f-428f-9b8f-2a7fc495b79f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2dee0f6a337cab7713862e662e06bb94a0b34a5d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124303"
---
# <a name="use-native-format-to-import-or-export-data-sql-server"></a>네이티브 형식을 사용하여 데이터 가져오기 및 내보내기(SQL Server)
  확장/DBCS(더블바이트 문자 집합) 문자가 포함되어 있지 않은 데이터 파일을 사용하여 여러 개의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 간에 데이터를 대량 전송할 때는 네이티브 형식을 사용하는 것이 바람직합니다.  
  
> [!NOTE]  
>  확장 또는 DBCS 문자가 포함되어 있는 데이터 파일을 사용하여 여러 개의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 간에 데이터를 대량 전송하려면 유니코드 네이티브 형식을 사용해야 합니다. 자세한 내용은 [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)을 참조하세요.  
  
 네이티브 형식은 데이터베이스의 원래 데이터 형식을 유지합니다. 네이티브 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 간에 데이터를 빠르게 전송하기 위한 형식입니다. 서식 파일을 사용할 경우 원본 및 대상 테이블의 형식이 동일할 필요가 없습니다. 데이터 전송은 두 단계로 이루어집니다.  
  
1.  원본 테이블에서 데이터 파일로 데이터 대량 내보내기  
  
2.  데이터 파일에서 대상 테이블로 데이터 대량 가져오기  
  
 형식이 동일한 테이블에서는 네이티브 형식을 사용하여 문자 형식의 불필요한 변환을 없애고 시간과 공간을 절약할 수 있습니다. 이때 최적의 전송 속도를 얻기 위해 데이터 형식을 거의 검사하지 않습니다. 로드된 데이터와 관련된 문제를 방지하려면 다음 제한 사항 목록을 참조하십시오.  
  
## <a name="restrictions"></a>Restrictions  
 데이터를 네이티브 형식으로 가져오려면 다음 사항을 확인하십시오.  
  
-   데이터 파일이 네이티브 형식인지 여부  
  
-   대상 테이블이 데이터 파일과 호환되는지 여부(예: 올바른 열 수, 데이터 형식, 길이, NULL 상태 등). 호환되지 않을 경우 각 필드를 해당 열에 매핑하기 위해 서식 파일을 사용해야 합니다.  
  
    > [!NOTE]  
    >  대상 테이블과 형식이 일치하지 않는 파일의 데이터를 가져오면 가져오기 작업에 성공하더라도 대상 테이블에 삽입된 데이터 값이 올바르지 않을 가능성이 높습니다. 이는 파일의 데이터가 대상 테이블의 서식을 사용하여 해석되기 때문입니다. 따라서 형식이 일치하지 않으면 잘못된 값이 삽입됩니다. 하지만 어떤 경우에도 이러한 불일치가 데이터베이스와의 논리적 또는 물리적 불일치를 유발하지는 않습니다.  
  
     서식 파일 사용에 대한 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)을 참조하세요.  
  
 데이터를 성공적으로 가져온 경우 대상 테이블은 손상되지 않습니다.  
  
## <a name="how-bcp-handles-data-in-native-format"></a>bcp의 네이티브 형식 데이터 처리 방법  
 이 섹션에서는 **bcp** 유틸리티가 데이터를 네이티브 형식으로 내보내고 가져오는 방법에 대한 특별한 고려 사항에 대해 설명합니다.  
  
-   문자가 아닌 데이터  
  
     bcp 유틸리티는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 binary 데이터 형식을 사용하여 문자가 아닌 테이블의 데이터를 데이터 파일에 기록합니다.  
  
-   `char` 또는 `varchar` 데이터  
  
     각 부분 `char` 나 `varchar` 필드 **bcp** 접두사 길이 추가 합니다.  
  
    > [!IMPORTANT]  
    >  기본적으로 네이티브 모드를 사용 하는 경우는 **bcp** 유틸리티가 문자에서 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 파일에 복사 하기 전에 OEM 문자로 합니다. 합니다 **bcp** 유틸리티가 문자 데이터 파일에서를 ANSI 문자로 변환 대량 가져오기 전에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다. 이러한 변환 과정에서 확장 문자 데이터가 손실될 수 있습니다. 확장 문자의 경우 유니코드 네이티브 형식을 사용하거나 코드 페이지를 지정하십시오.  
  
-   `sql_variant` 데이터  
  
     경우 `sql_variant` 데이터 네이티브 형식 데이터 파일에 SQLVARIANT로 저장 되므로, 해당 특성을 모두 유지 합니다. 각 데이터 값의 데이터 형식을 기록하는 메타데이터는 데이터 값과 함께 저장됩니다. 이 메타 데이터는 다시 대상에 동일한 데이터 형식 가진 데이터 값을 만드는 데 `sql_variant` 열입니다.  
  
     대상 열의 데이터 형식이 없으면 `sql_variant`, 각 데이터 값은 암시적 데이터 변환 규칙에 따라 대상 열의 데이터 형식으로 변환 됩니다. 데이터 변환 중에 오류가 발생하면 현재 일괄 처리가 롤백됩니다. `char` 열 간에 전송되는 모든 `varchar` 및 `sql_variant` 값에는 코드 페이지 변환 문제가 있을 수 있습니다.  
  
     데이터 변환에 대한 자세한 내용은 [데이터 형식 변환&#40;데이터베이스 엔진&#41;](/sql/t-sql/data-types/data-type-conversion-database-engine)을 참조하세요.  
  
## <a name="command-options-for-native-format"></a>네이티브 형식의 명령 옵션  
 **bcp**, BULK INSERT 또는 INSERT ... SELECT \* FROM OPENROWSET(BULK...)를 사용하여 테이블로 유니코드 원시 형식 데이터를 가져올 수 있습니다. **bcp** 명령 또는 BULK INSERT 문의 경우 명령줄에서 데이터 형식을 지정할 수 있습니다. INSERT ... SELECT * FROM OPENROWSET(BULK...) 문의 경우 서식 파일에서 데이터 형식을 지정해야 합니다.  
  
 네이티브 형식에 대해 지원되는 명령줄 옵션은 다음과 같습니다.  
  
|Command|옵션|Description|  
|-------------|------------|-----------------|  
|**bcp**|**-n**|발생 합니다 **bcp** 유틸리티가 네이티브 데이터 형식의 데이터를 사용 하도록 합니다.<sup> 1</sup>|  
|BULK INSERT|DATAFILETYPE **='** native **'**|데이터의 네이티브 또는 와이드 네이티브 데이터 형식을 사용합니다. 서식 파일로 데이터 형식을 지정하면 DATAFILETYPE은 필요하지 않습니다.|  
  
 <sup>1</sup> 네이티브 로드 (**-n**)의 이전 버전과 호환 되는 형식에 대 한 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트를 사용 하 여 합니다 **-V** 전환 합니다. 자세한 내용은 [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)를 참조하세요.  
  
 자세한 내용은 [bcp 유틸리티](../../tools/bcp-utility.md), [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) 또는 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)를 참조하세요.  
  
> [!NOTE]  
>  서식 파일에서 필드 단위로 서식을 지정할 수도 있습니다. 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)를 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 **bcp** 를 사용하여 네이티브 데이터의 대량 내보내기를 수행하고 내보낸 데이터에 BULK INSERT를 사용하여 대량 가져오기를 수행하는 방법을 보여 줍니다.  
  
### <a name="sample-table"></a>예제 테이블  
 이 예에서는 **dbo** 스키마에서 **AdventureWorks** 예제 데이터베이스에 **myTestNativeData** 라는 이름의 테이블을 만들어야 합니다. 예를 실행하려면 이 테이블을 만들어야 합니다. [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음을 실행합니다.  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestNativeData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 이 테이블을 채우고 결과 내용을 확인하려면 다음 문을 실행합니다.  
  
```  
INSERT INTO myTestNativeData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestNativeData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestNativeData  
  
```  
  
### <a name="using-bcp-to-bulk-export-native-data"></a>bcp를 사용하여 네이티브 데이터 대량 내보내기  
 테이블의 데이터를 데이터 파일로 내보내려면 **out** 옵션 및 다음 한정자가 있는 **bcp** 를 사용합니다.  
  
|한정자|Description|  
|----------------|-----------------|  
|**-n**|네이티브 데이터 형식을 지정합니다.|  
|**-T**|**bcp** 유틸리티가 통합 보안을 사용하는 트러스트된 연결을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 연결되도록 지정합니다. **-T** 를 지정하지 않은 경우 성공적으로 로그인하려면 **-U** 와 **-P** 를 지정해야 합니다.|  
  
 다음 예에서는 `myTestNativeData` 테이블에서 `myTestNativeData-n.Dat` 데이터 파일로 네이티브 형식의 데이터를 대량으로 내보냅니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 명령 프롬프트에 다음을 입력합니다.  
  
```  
bcp AdventureWorks..myTestNativeData out C:\myTestNativeData-n.Dat -n -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-native-data"></a>BULK INSERT를 사용하여 네이티브 데이터 대량 가져오기  
 다음 예에서는 BULK INSERT를 사용하여 `myTestNativeData-n.Dat` 데이터 파일의 데이터를 `myTestNativeData` 테이블로 가져옵니다. [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음을 실행합니다.  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestNativeData   
    FROM 'C:\myTestNativeData-n.Dat'   
   WITH (DATAFILETYPE='native');   
GO  
SELECT Col1,Col2,Col3 FROM myTestNativeData  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **대량 가져오기 또는 대량 내보내기를 위한 데이터 형식을 사용하려면**  
  
-   [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [데이터 형식&#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [sql_variant&#40;Transact-SQL&#41;](/sql/t-sql/data-types/sql-variant-transact-sql)   
 [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
  
