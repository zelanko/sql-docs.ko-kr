---
title: 문자 형식을 사용하여 데이터 가져오기 및 내보내기(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], character
- character formats [SQL Server]
ms.assetid: d925e66a-1a73-43cd-bc06-1cbdf8174a4d
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a4249f87cf7a8361056caf6c49b3775848d7dfe5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37250193"
---
# <a name="use-character-format-to-import-or-export-data-sql-server"></a>문자 형식을 사용하여 데이터 가져오기 및 내보내기(SQL Server)
  다른 프로그램에서 사용할 텍스트 파일로 데이터를 대량으로 내보내거나 다른 프로그램에서 생성한 텍스트 파일에서 데이터를 대량으로 가져오는 경우 문자 형식을 사용하는 것이 좋습니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 유니코드 문자 데이터는 포함하지만 확장 문자 또는 DBCS(더블바이트 문자 집합) 문자는 포함하지 않는 데이터 파일 간에 데이터를 대량 전송하는 경우에는 유니코드 문자 형식을 사용하세요. 자세한 내용은 [유니코드 문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)를 참조하세요.  
  
 문자 형식은 모든 열에 문자 데이터 형식을 사용합니다. 스프레드시트 등의 다른 프로그램에서 데이터를 사용하거나 Oracle 등의 다른 데이터베이스의 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 복사할 때는 문자 형식으로 정보를 저장하십시오.  
  
## <a name="considerations-for-using-character-format"></a>문자 형식 사용 시 고려 사항  
 문자 형식을 사용할 때 다음 사항을 고려하십시오.  
  
-   기본적으로 **bcp** 유틸리티는 탭 문자로 문자 데이터 필드를 구분하며 줄 바꿈 문자로 레코드를 종료합니다. 다른 종결자를 지정하는 방법에 대한 자세한 내용은 [필드 및 행 종결자 지정&#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)을 참조하세요.  
  
-   기본적으로 문자 모드의 데이터를 대량으로 내보내거나 대량으로 가져오기 전에 다음 변환이 수행됩니다.  
  
    |대량 작업의 방향|변환|  
    |---------------------------------|----------------|  
    |내보내기|데이터를 문자 표시로 변환합니다. 명시적으로 요청한 경우 문자 열에 요청한 코드 페이지로 데이터를 변환합니다. 코드 페이지를 지정하지 않으면 클라이언트 컴퓨터의 OEM 코드 페이지를 사용하여 문자 데이터를 변환합니다.|  
    |가져오기|필요한 경우 먼저 문자 데이터를 네이티브 표시로 변환하고 클라이언트의 코드 페이지에서 대상 열의 코드 페이지로 문자 데이터를 변환합니다.|  
  
-   변환 작업 중에 확장 문자가 손실되는 것을 방지하려면 유니코드 문자 형식을 사용하거나 코드 페이지를 지정하십시오.  
  
-   문자 서식 파일로 저장되는 모든 `sql_variant` 데이터는 메타데이터 없이 저장됩니다. 각 데이터 값으로 변환 됩니다 `char` 암시적 데이터 변환 규칙에 따라 합니다. `sql_variant` 열로 데이터를 가져오는 경우 `char`로 변환됩니다. 이외의 다른 데이터 형식의 열으로 가져올 때 `sql_variant`에서 변환 되는 데이터 `char` 암시적 변환을 사용 하 여 합니다. 데이터 변환에 대한 자세한 내용은 [데이터 형식 변환&#40;데이터베이스 엔진&#41;](/sql/t-sql/data-types/data-type-conversion-database-engine)을 참조하세요.  
  
-   합니다 **bcp** 유틸리티 내보내기 `money` 4 자리만 표시 하며 쉼표 구분자 등 모든 자릿수 구분 기호 없이 소수점 문자 형식 데이터 파일로 값입니다. 예를 들어 1,234,567.123456이라는 값을 포함하는 `money` 열을 데이터 파일로 대량 내보내면 1234567.1235라는 문자열이 됩니다.  
  
## <a name="command-options-for-character-format"></a>문자 형식의 명령 옵션  
 **bcp**, BULK INSERT 또는 INSERT ...를 사용하여 문자 형식 데이터를 테이블로 가져올 수 있습니다. SELECT \* FROM OPENROWSET(BULK...)를 사용하여 테이블로 유니코드 원시 형식 데이터를 가져올 수 있습니다. **bcp** 명령 또는 BULK INSERT 문의 경우 명령줄에서 데이터 형식을 지정할 수 있습니다. INSERT ... SELECT * FROM OPENROWSET(BULK...) 문의 경우 서식 파일에서 데이터 형식을 지정해야 합니다.  
  
 다음 명령줄 옵션으로 문자 형식을 사용할 수 있습니다.  
  
|Command|옵션|Description|  
|-------------|------------|-----------------|  
|**bcp**|**-c**|발생 합니다 **bcp** 유틸리티가 문자 데이터를 사용 하도록 합니다.<sup> 1</sup>|  
|BULK INSERT|DATAFILETYPE **='char'**|데이터를 대량 가져올 때 문자 형식을 사용합니다.|  
  
 <sup>1</sup> 문자를 로드 하려면 (**-c**)의 이전 버전과 호환 되는 형식에 대 한 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트를 사용 하 여는 **-V** 전환 합니다. 자세한 내용은 [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)를 참조하세요.  
  
 자세한 내용은 [bcp 유틸리티](../../tools/bcp-utility.md), [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) 또는 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)를 참조하세요.  
  
> [!NOTE]  
>  서식 파일에서 필드 단위로 서식을 지정할 수도 있습니다. 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)를 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 **bcp** 를 사용하여 문자 데이터의 대량 내보내기를 수행하고 내보낸 데이터에 BULK INSERT를 사용하여 대량 가져오기를 수행하는 방법을 보여 줍니다.  
  
### <a name="sample-table"></a>예제 테이블  
 이 예에서는 **dbo** 스키마의 **AdventureWorks** 예제 데이터베이스에 **myTestCharData** 라는 테이블이 필요하며 예를 실행하려면 이 테이블을 만들어야 합니다. SQL에서이 테이블을 만들려면 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 실행 합니다.  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestCharData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 이 테이블을 채우고 결과 내용을 확인하려면 다음 문을 실행합니다.  
  
```  
INSERT INTO myTestCharData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestCharData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestCharData  
  
```  
  
### <a name="using-bcp-to-bulk-export-character-data"></a>bcp를 사용하여 문자 데이터 대량 내보내기  
 테이블의 데이터를 데이터 파일로 내보내려면 **out** 옵션 및 다음 한정자가 있는 **bcp** 를 사용합니다.  
  
|한정자|Description|  
|----------------|-----------------|  
|**-c**|문자 형식을 지정합니다.|  
|**-t** `,`|쉼표(`,`)를 필드 종결자로 지정합니다.<br /><br /> 참고: 기본 필드 종결자는 탭 문자(\t)입니다. 자세한 내용은 [필드 및 행 종결자 지정&#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)을 참조하세요.|  
|**-T**|**bcp** 유틸리티가 통합 보안을 사용하는 트러스트된 연결을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 연결되도록 지정합니다. **-T**를 지정하지 않은 경우 성공적으로 로그인하려면 **-U**와 **-P**를 지정해야 합니다.|  
  
 다음 예에서는 `myTestCharData` 테이블에서 쉼표(,)를 필드 종결자로 사용하는 `myTestCharData-c.Dat`라는 새 데이터 파일로 문자 형식의 데이터를 대량으로 내보냅니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 명령 프롬프트에 다음을 입력합니다.  
  
```  
bcp AdventureWorks..myTestCharData out C:\myTestCharData-c.Dat -c -t, -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-character-data"></a>BULK INSERT를 사용하여 문자 데이터 대량 가져오기  
 다음 예에서는 BULK INSERT를 사용하여 `myTestCharData-c.Dat` 데이터 파일의 데이터를 `myTestCharData` 테이블로 가져옵니다. [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음을 실행합니다.  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestCharData   
   FROM 'C:\myTestCharData-c.Dat'   
   WITH (  
      DATAFILETYPE='char',  
      FIELDTERMINATOR=','  
   );   
GO  
SELECT Col1,Col2,Col3 FROM myTestCharData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **대량 가져오기 또는 대량 내보내기를 위한 데이터 형식을 사용하려면**  
  
-   [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [네이티브 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>관련 항목  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [데이터 형식&#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
  
