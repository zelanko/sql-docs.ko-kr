---
title: bcp 유틸리티 | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server]
- exporting data
- row exporting [SQL Server]
- copying data [SQL Server], bcp utility
- command prompt utilities [SQL Server], bcp
- tables [SQL Server], importing data
- column importing [SQL Server]
- bcp utility [SQL Server], command options
- file exporting [SQL Server]
- bulk copy [SQL Server]
- bcp utility [SQL Server], about bcp utility
- tables [SQL Server], exporting data
- row importing [SQL Server]
- importing data, bcp utility
- file importing [SQL Server]
- column exporting [SQL Server]
ms.assetid: c0af54f5-ca4a-4995-a3a4-0ce39c30ec38
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0ddc4c4e7023a83bfde9295a1410e7db5cb90b84
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85008744"
---
# <a name="bcp-utility"></a>bcp 유틸리티
  **Bcp** 유틸리티는 인스턴스와 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용자가 지정한 형식의 데이터 파일 간에 데이터를 대량 복사 합니다. **bcp** 유틸리티를 사용하여 많은 수의 새 행을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 테이블로 가져오거나 테이블에서 데이터 파일로 데이터를 내보낼 수 있습니다. **queryout** 옵션과 함께 사용하는 경우를 제외하고 이 유틸리티를 사용하는 데에는 [!INCLUDE[tsql](../includes/tsql-md.md)]에 대한 지식이 필요하지 않습니다. 테이블로 데이터를 가져오려면 해당 테이블에 대해 만든 서식 파일을 사용하거나 이 테이블의 열에 적합한 테이블 구조와 데이터 형식을 알아야 합니다.  
  
 ![항목 링크 아이콘](../../2014/database-engine/media/topic-link.gif "항목 링크 아이콘")**bcp** 구문에 사용되는 구문 표기 규칙에 대한 자세한 내용은 [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql)을 참조하세요.  
  
> [!NOTE]  
>  **bcp** 를 사용하여 데이터를 백업하는 경우 서식 파일을 만들어 데이터 서식을 기록합니다. **bcp** 데이터 파일에는 스키마 또는 서식 정보가 포함되어 있지 않기 때문에 테이블이나 뷰가 삭제된 경우 서식 파일이 없으면 데이터를 가져오지 못할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
   bcp [database_name.] schema.{table_name | view_name | "query" {indata_file | outdata_file | queryoutdata_file | format nul}  
  
[-apacket_size]  
[-bbatch_size]  
[-c]  
[-C { ACP | OEM | RAW | code_page } ]  
[-ddatabase_name]  
[-eerr_file]  
[-E]  
[-fformat_file]  
[-Ffirst_row]  
[-h"hint [,...n]"]   
[-iinput_file]  
[-k]  
[-Kapplication_intent]  
[-Llast_row]  
[-mmax_errors]  
[-n]  
[-N]  
[-ooutput_file]  
[-Ppassword]  
[-q]  
[-rrow_term]  
[-R]  
[-S [server_name[\instance_name]]  
[-tfield_term]  
[-T]  
[-Ulogin_id]  
[-v]  
[-V (80 | 90 | 100 | 110)]  
[-w]  
[-x]  
/?  
```  
  
## <a name="arguments"></a>인수  
 *data_file*  
 데이터 파일의 전체 경로입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 데이터를 대량으로 가져오는 경우 데이터 파일에는 지정한 테이블 또는 뷰로 복사할 데이터가 포함됩니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 데이터를 대량으로 내보내는 경우 데이터 파일에는 테이블 또는 뷰에서 복사한 데이터가 포함됩니다. 데이터 파일 경로는 1에서 255자까지 포함할 수 있습니다. 데이터 파일에는 최대 2 개의<sup>63</sup> -1 개의 행이 포함 될 수 있습니다.  
  
 *database_name*  
 지정한 테이블 또는 뷰가 있는 데이터베이스의 이름입니다. 이 인수를 지정하지 않으면 사용자의 기본 데이터베이스를 사용합니다.  
  
 `d-`를 사용하여 데이터베이스 이름을 명시적으로 지정할 수도 있습니다.  
  
 **in** _data_file_  |  **out**_data_file_  |  **queryout**_data_file_  |  **형식 nul**  
 다음과 같이 대량 복사 방향을 지정합니다.  
  
-   **in** 은 파일에서 데이터베이스 테이블 또는 뷰로 복사합니다.  
  
-   **out** 은 데이터베이스 테이블 또는 뷰에서 파일로 복사합니다. 기존 파일을 지정하면 이 파일을 덮어씁니다. 데이터를 추출할 때 **bcp** 유틸리티는 빈 문자열을 null로 나타내고 null 문자열은 빈 문자열로 나타냅니다.  
  
-   **queryout** 은 쿼리에서 복사하며 쿼리에서 데이터를 대량 복사하는 경우에만 지정해야 합니다.  
  
-   **format** 은 지정 된 옵션 (**-n**, `-c` , `-w` 또는 **-n**)과 테이블 또는 뷰 구분 기호를 기반으로 서식 파일을 만듭니다. 데이터를 대량 복사 하는 경우 **bcp** 명령은 서식 파일을 참조할 수 있으므로 대화형으로 서식 정보를 다시 입력할 필요가 없습니다. **format** 옵션에는 **-f** 옵션이 필요하며 XML 서식 파일을 만드는 경우 **-x** 옵션도 필요합니다. 자세한 내용은 [서식 파일 만들기&#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md)를 참조하세요. **nul** 을 값으로 지정해야 합니다(**format nul**).  
  
 *owner*  
 테이블 또는 뷰의 소유자 이름입니다. 작업을 수행하는 사용자가 지정한 테이블 또는 뷰를 소유하고 있는 경우에는*owner* 를 생략할 수 있습니다. *owner* 를 지정하지 않은 경우 작업을 수행하는 사용자가 지정한 테이블이나 뷰의 소유자가 아니면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 오류 메시지를 반환하고 작업이 취소됩니다.  
  
 **"** _쿼리_ **"**  
 결과 집합을 반환하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리입니다. 쿼리에서 여러 결과 집합을 반환하는 경우 첫 번째 결과 집합만 데이터 파일에 복사되고 그 다음 결과 집합은 무시됩니다. 쿼리는 큰따옴표로 묶고 쿼리 안에 포함되는 모든 것은 작은따옴표로 묶습니다. 쿼리에서 데이터를 대량 복사할 때는**queryout** 도 지정해야 합니다.  
  
 쿼리는 bcp 문을 실행하기 전에 저장 프로시저 내에서 참조되는 모든 테이블이 존재하는 한 저장 프로시저를 참조할 수 있습니다. 예를 들어 저장 프로시저가 임시 테이블을 생성하면 이 임시 테이블을 런타임에만 사용할 수 있고 문 실행 시에는 사용할 수 없기 때문에 **bcp** 문이 실패합니다. 이 경우 테이블에 저장 프로시저 결과를 삽입한 다음 **bcp** 를 사용하여 테이블에서 데이터 파일로 데이터를 복사할 수 있습니다.  
  
 *table_name*  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로 데이터를 가져올 때(**in**)는 대상 테이블의 이름이고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 데이터를 내보낼 때(**out**)는 원본 테이블의 이름입니다.  
  
 *view_name*  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로 데이터를 복사할 때(**in**)는 대상 뷰의 이름이고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 데이터를 복사할 때(**out**)는 원본 뷰의 이름입니다. 모든 열이 같은 테이블을 참조하는 뷰만 대상 뷰로 사용할 수 있습니다. 뷰에 데이터를 복사하는 경우의 제한 사항에 대한 자세한 내용은 [INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)를 참조하세요.  
  
 **-a** _packet_size_  
 서버에서 전송되거나 서버로 전송되는 네트워크 패킷당 바이트 수를 지정합니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 또는 **sp_configure** 시스템 저장 프로시저를 사용하여 서버 구성 옵션을 설정할 수 있습니다. 그러나 이 옵션을 사용하여 서버 구성 옵션을 개별적으로 재정의할 수 있습니다. *packet_size* 는 4096 ~ 65535바이트일 수 있고 기본값은 4096입니다.  
  
 패킷 크기가 커지면 대량 복사 작업의 성능이 향상될 수 있습니다. 더 큰 패킷을 요청했는데 허용되지 않으면 기본값이 사용됩니다. **bcp** 유틸리티가 생성하는 성능 통계에는 사용되는 패킷의 크기가 나타납니다.  
  
 **-b** _batch_size_  
 가져온 데이터의 일괄 처리당 행 수를 지정합니다. 각 일괄 처리는 커밋되기 전에 전체 일괄 처리를 가져오는 별도의 트랜잭션으로 가져오고 기록합니다. 기본적으로 데이터 파일의 모든 행은 하나의 일괄 처리로 가져옵니다. 여러 일괄 처리에 행을 분산시키려면 데이터 파일의 행 수보다 작은 *batch_size* 를 지정합니다. 일괄 처리에 대한 트랜잭션이 실패하면 현재 일괄 처리에서 삽입한 내용만 롤백됩니다. 커밋된 트랜잭션으로 이미 가져온 일괄 처리는 나중에 발생한 오류의 영향을 받지 않습니다.  
  
 이 옵션을 **-h "** ROWS_PER_BATCH ** = *`bb`* "** 옵션과 함께 사용 하지 마세요.  
  
 `-c`  
 문자 데이터 형식을 사용하여 작업을 수행합니다. 이 옵션은 각 필드에 대해 묻지 않습니다. `char`접두사와 **\t** (탭 문자)를 필드 구분 기호로 사용 하지 않고 **\r\n** (줄 바꿈 문자)을 행 종결자로 사용 하 여을 저장소 유형으로 사용 합니다. `-c`는 `-w`와 호환되지 않습니다.  
  
 자세한 내용은 [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)를 참조하세요.  
  
 **-C** { **ACP** | **OEM** | **RAW** | *code_page* }  
 데이터 파일에서 데이터의 코드 페이지를 지정합니다. *code_page* 는 `char` `varchar` `text` 문자 값이 127 보다 크거나 32 보다 작은, 또는 열이 데이터에 포함 되어 있는 경우에만 해당 됩니다.  
  
> [!NOTE]  
>  서식 파일의 각 열에 대해 데이터 정렬 이름을 지정하는 것이 좋습니다.  
  
|코드 페이지 값|Description|  
|---------------------|-----------------|  
|ACP|[!INCLUDE[vcpransi](../includes/vcpransi-md.md)]/Microsoft Windows(ISO 1252)입니다.|  
|OEM|클라이언트가 사용하는 기본 코드 페이지입니다. **-C** 를 지정하지 않은 경우 사용되는 기본 코드 페이지입니다.|  
|RAW|코드 페이지 간 변환이 일어나지 않습니다. 변환이 일어나지 않으므로 가장 빠른 옵션입니다.|  
|*code_page*|850과 같은 특정 코드 페이지 번호입니다.<br /><br /> **&#42;&#42; 중요 &#42;&#42;** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 코드 페이지 65001 (UTF-8 인코딩)을 지원 하지 않습니다.|  
  
 `-d`*database_name*  
 연결할 데이터베이스를 지정합니다. bcp.exe는 기본적으로 사용자의 기본 데이터베이스에 연결됩니다. `-d` *Database_name* 와 세 부분으로 구성 된 이름 (bcp.exe의 첫 번째 매개 변수로 전달 된*database_name*)을 지정 하면 데이터베이스 이름을 두 번 지정할 수 없으므로 오류가 발생 합니다. *Database_name* 하이픈 (-) 또는 슬래시 (/)로 시작 하는 경우와 데이터베이스 이름 사이에 공백을 추가 하지 마십시오 `-d` .  
  
 **-e** _err_file_  
 **bcp** 유틸리티가 파일에서 데이터베이스로 전송할 수 없는 행을 저장하는 데 사용되는 오류 파일의 전체 경로를 지정합니다. **bcp** 명령의 오류 메시지는 사용자의 워크스테이션에 나타납니다. 이 옵션을 사용하지 않으면 오류 파일이 생성되지 않습니다.  
  
 *err_file* 이 하이픈(-) 또는 슬래시(/)로 시작하는 경우에는 **-e** 와 *err_file* 값 사이에 공백을 포함하지 마세요.  
  
 **-E**  
 가져온 데이터 파일의 ID 값이 ID 열에 사용되도록 지정합니다. **-E** 를 지정하지 않으면 가져오는 데이터 파일에 있는 이 열의 ID 값이 무시되고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 테이블을 만들 때 지정한 초기값 및 증가값을 기반으로 고유 값을 자동으로 할당합니다.  
  
 데이터 파일에 테이블이나 뷰의 ID 열 값이 포함되지 않은 경우 서식 파일을 사용하여 데이터를 가져올 때 테이블이나 뷰의 ID 열을 생략하도록 지정합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 해당 열에 자동으로 고유 값을 할당합니다. 자세한 내용은 [DBCC CHECKIDENT&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql)를 참조하세요.  
  
 **-E** 옵션을 사용하려면 특별한 권한이 있어야 합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
 **-f** _format_file_  
 서식 파일의 전체 경로를 지정합니다. 다음과 같이 이 옵션의 의미는 해당 환경에 따라 다릅니다.  
  
-   **format** 옵션과 함께 **-f** 를 사용하는 경우 지정한 테이블 또는 뷰에 대해 지정한 *format_file* 이 만들어집니다. XML 서식 파일을 만들려면 **-x** 옵션도 지정합니다. 자세한 내용은 [서식 파일 만들기&#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md)를 참조하세요.  
  
-   **-f** 를 **in** 또는 **out** 옵션과 함께 사용하는 경우 기존 서식 파일이 필요합니다.  
  
    > [!NOTE]  
    >  원할 경우 **in** 또는 **out** 옵션과 함께 서식 파일을 사용할 수도 있습니다. - **F** 옵션이 없을 경우 **-n**, `-c` , `-w` 또는 **-n** 을 지정 하지 않으면 명령에서 형식 정보를 묻는 메시지를 표시 하 고 응답을 서식 파일에 저장할 수 있습니다 (기본 파일 이름은 Bcp. fmt).  
  
 *format_file* 이 하이픈(-) 또는 슬래시(/)로 시작하는 경우에는 **-f** 와 *format_file* 값 사이에 공백을 포함하지 마세요.  
  
 **-F** _first_row_  
 테이블에서 내보내거나 데이터 파일에서 가져올 첫 번째 행 번호를 지정합니다. 이 매개 변수에는 (>) 0 보다 크고 () 보다 작거나 ( \< =) 총 행 수와 같은 값이 필요 합니다. 이 매개 변수를 지정하지 않을 경우 기본값은 파일의 첫 번째 행입니다.  
  
 *first_row* 는 최대 2^63-1의 값을 갖는 양의 정수입니다. **-F**_first_row_는 1부터 시작합니다.  
  
 **-h"** _hint_[ **,**... *n*] **"**  
 데이터를 테이블 또는 뷰로 대량으로 가져올 때 사용할 힌트를 지정합니다.  
  
 ORDER **(**_column_[ASC | DESC] [**,**... *n*] **)**  
 데이터 파일에 있는 데이터의 정렬 순서입니다. 가져올 데이터를 테이블의 클러스터형 인덱스(있는 경우)에 따라 정렬하면 대량 가져오기 성능이 향상됩니다. 데이터 파일을 클러스터형 인덱스 키와 다른 순서로 정렬하거나 테이블에 클러스터형 인덱스가 없으면 ORDER 절이 무시됩니다. 지정한 열 이름은 대상 테이블에서 올바른 열 이름이어야 합니다. 기본적으로 **bcp** 는 데이터 파일이 정렬되지 않은 것으로 간주합니다. 대량 가져오기 작업을 최적화하기 위해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서는 가져온 데이터가 정렬되어 있는지도 확인합니다.  
  
 ROWS_PER_BATCH **=** _bb_  
 일괄 처리당 데이터 행 수( *bb*)입니다. **-b** 를 지정하지 않은 경우에 사용되며 전체 데이터 파일을 단일 트랜잭션으로 서버에 보냅니다. 서버는 *bb*값에 따라 대량 로드를 최적화합니다. 기본적으로 ROWS_PER_BATCH는 알 수 없습니다.  
  
 KILOBYTES_PER_BATCH **=** _참조_  
 일괄 처리당 데이터의 대략적인 KB 단위 크기( *cc*)입니다. 기본적으로 KILOBYTES_PER_BATCH는 알 수 없습니다.  
  
 TABLOCK  
 대량 로드 작업이 진행되는 동안 대량 업데이트 테이블 수준 잠금이 사용되도록 지정합니다. 그렇지 않으면 행 수준 잠금이 사용됩니다. 대량 복사 작업 중에 잠금을 보유하면 테이블의 잠금 경합이 줄어들기 때문에 이 힌트를 사용하면 성능이 크게 향상됩니다. 테이블에 인덱스가 없고 **TABLOCK** 이 지정되어 있으면 여러 클라이언트가 동시에 테이블을 로드할 수 있습니다. 기본적으로 잠금 동작은 **table lock on bulk load**테이블 옵션에 의해 결정됩니다.  
  
 CHECK_CONSTRAINTS  
 대량 가져오기 작업 중 대상 테이블 또는 뷰의 모든 제약 조건을 검사하도록 지정합니다. CHECK_CONSTRAINTS 힌트를 지정하지 않으면 모든 CHECK 및 FOREIGN KEY 제약 조건이 무시되며 작업 후 테이블의 제약 조건은 트러스트되지 않는 것으로 표시됩니다.  
  
> [!NOTE]  
>  UNIQUE, PRIMARY KEY 및 NOT NULL 제약 조건은 항상 적용됩니다.  
  
 어느 시점에서는 전체 테이블의 제약 조건을 확인할 필요가 있습니다. 대량 가져오기 작업을 수행하기 전에 테이블이 비어 있지 않은 경우 제약 조건의 유효성을 다시 검사하는 비용이 증분 데이터에 CHECK 제약 조건을 적용하는 비용을 초과할 수 있습니다. 따라서 일반적으로 증분 대량 가져오기 중에 제약 조건을 검사하도록 설정하는 것이 좋습니다.  
  
 입력 데이터에 제약 조건을 위반하는 행이 포함된 경우에는 제약 조건을 사용하지 않을 수 있습니다(기본 동작). CHECK 제약 조건을 사용하지 않으면 데이터를 가져온 다음 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 사용하여 잘못된 데이터를 제거할 수 있습니다.  
  
> [!NOTE]  
>  **bcp** 는 이제 데이터 유효성 검사 및 데이터 검사를 강제로 실행하므로 스크립트를 데이터 파일의 잘못된 데이터에 대해 실행할 경우 오류가 발생할 수 있습니다.  
  
> [!NOTE]  
>  **-m** _max_errors_ 스위치는 제약 조건 검사에 적용되지 않습니다.  
  
 FIRE_TRIGGERS  
 **in** 인수와 함께 지정하면 대량 복사 작업 중에 대상 테이블에 정의한 삽입 트리거가 실행됩니다. FIRE_TRIGGERS를 지정하지 않으면 삽입 트리거가 실행되지 않습니다. FIRE_TRIGGERS는 **out**, **queryout**및 **format** 인수에 대해 무시됩니다.  
  
 **-i** _input_file_  
 대화형 모드를 사용 하 여 대량 복사를 수행할 때 각 데이터 필드에 대 한 명령 프롬프트 질문에 대 한 응답을 포함 하는 지시 파일의 이름을 지정 합니다 (**-n**, `-c` , `-w` 또는 **-n** 을 지정 하지 않음).  
  
 *input_file* 이 하이픈(-) 또는 슬래시(/)로 시작하는 경우에는 **-i** 와 *input_file* 값 사이에 공백을 포함하지 마세요.  
  
 **-k**  
 작업 시 삽입된 열에 기본값이 지정되지 않고 빈 열이 Null 값을 보유하도록 지정합니다. 자세한 내용은 [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)을 참조하세요.  
  
 **-K** _application_intent_  
 서버에 연결할 때 애플리케이션 작업 유형을 선언합니다. **ReadOnly**값만 사용할 수 있습니다. **-K**를 지정하지 않으면 bcp 유틸리티가 AlwaysOn 가용성 그룹에 있는 보조 복제본에 연결할 수 없습니다. 자세한 내용은 [활성 보조: 읽기 가능한 보조 복제본 (AlwaysOn 가용성 그룹)](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)을 참조 하세요.  
  
 **-L** _last_row_  
 테이블에서 내보내거나 데이터 파일에서 가져올 마지막 행 번호를 지정합니다. 이 매개 변수에는 (>) 0 보다 크고 () 보다 작거나 ( \< =) 마지막 행 번호 보다 작거나 같은 값이 필요 합니다. 이 매개 변수를 지정하지 않을 경우 기본값은 파일의 마지막 행입니다.  
  
 *last_row* 는 최대 2^63-1의 값을 갖는 양의 정수입니다.  
  
 **-m** _max_errors_  
 **bcp** 작업이 취소되는 최대 구문 오류 발생 횟수를 지정합니다. 구문 오류란 대상 데이터 형식으로의 데이터 변환 오류를 나타냅니다. 총 *max_errors* 수에는 제약 조건 위반과 같이 서버에서만 검색할 수 있는 오류는 제외됩니다.  
  
 **bcp** 유틸리티가 복사할 수 없는 행은 무시되며 오류가 하나 발생한 것으로 간주됩니다. 이 옵션을 지정하지 않은 경우의 기본값은 10입니다.  
  
> [!NOTE]  
>  **-M** 옵션은 `money` 또는 데이터 형식을 변환 하는 데에도 적용 되지 않습니다 `bigint` .  
  
 **-n**  
 데이터의 네이티브(데이터베이스) 데이터 형식을 사용하여 대량 복사 작업을 수행합니다. 이 옵션이 필드마다 표시되지는 않습니다. 이 옵션은 네이티브 값을 사용합니다.  
  
 자세한 내용은 [네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)를 참조하세요.  
  
 **-N**  
 문자가 아닌 데이터의 경우 데이터의 네이티브(데이터베이스) 데이터 형식을 사용하고 문자 데이터의 경우 유니코드 문자를 사용하여 대량 복사 작업을 수행합니다. 이 옵션은 `-w` 옵션을 사용할 때보다 성능이 높으며 데이터 파일을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 간에 데이터를 전송할 때 사용할 수 있습니다. 이 옵션은 각 필드에 대한 정보를 요청하지 않습니다. ANSI 확장 문자가 들어 있는 데이터를 전송하는 경우 기본 모드의 성능을 활용하려고 할 때 이 옵션을 사용하십시오.  
  
 자세한 내용은 [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)을 참조하세요.  
  
 **-N**과 함께 bcp.exe를 사용 하 여 동일한 테이블 스키마에 데이터를 내보낸 다음 가져올 경우 비유니코드 고정 길이 문자 열 (예:)이 있으면 잘림 경고가 표시 될 수 있습니다 `char(10)` .  
  
 이 경고는 무시해도 됩니다. **-N** 대신 **-n**을 사용하여 이 경고를 해결할 수 있습니다.  
  
 **-o** _output_file_  
 명령 프롬프트에서 리디렉션된 출력을 받는 파일의 이름을 지정합니다.  
  
 *output_file* 이 하이픈(-) 또는 슬래시(/)로 시작하는 경우에는 **-o** 와 *output_file* 값 사이에 공백을 포함하지 마세요.  
  
 **-P** _password_  
 로그인 ID의 암호를 지정합니다. 이 옵션을 사용하지 않으면 **bcp** 명령을 실행하는 동안 암호를 묻는 메시지가 표시됩니다. 암호를 입력하지 않고 명령 프롬프트의 마지막에 이 옵션을 사용하면 **bcp** 는 기본 암호 NULL을 사용합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]  
  
 암호를 마스킹하려면 **-U** 옵션과 함께 **-P** 옵션을 지정하지 마세요. 대신 **-U** 옵션 및 기타 스위치와 함께 **bcp** 를 지정하고( **-P**는 지정하지 않음) Enter 키를 누르면 암호를 묻는 메시지가 표시됩니다. 이 방법을 사용하면 암호 입력 시 암호가 마스킹됩니다.  
  
 *password* 가 하이픈(-) 또는 슬래시(/)로 시작하는 경우에는 **-P** 와 *password* 값 사이에 공백을 포함하지 마세요.  
  
 `-q`  
 **bcp** 유틸리티와 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스 간의 연결에서 SET QUOTED_IDENTIFIERS ON 문을 실행합니다. 이 옵션을 사용하여 공백이나 작은따옴표를 포함하는 데이터베이스, 소유자, 테이블 또는 뷰 이름을 지정합니다. 세 부분으로 구성된 테이블 이름이나 뷰 이름 전체를 큰따옴표("")로 묶습니다.  
  
 공백이나 작은따옴표가 들어 있는 데이터베이스 이름을 지정하려면 **–q** 옵션을 사용해야 합니다.  
  
 `-q`는 `-d`로 전달된 값에는 적용되지 않습니다.  
  
 자세한 내용은 이 항목의 뒷부분에 나오는 주의를 참조하십시오.  
  
 **-r** _row_term_  
 행 종결자를 지정합니다. 기본값은 **\n** (줄 바꿈 문자)입니다. 기본 행 종결자를 재정의하려면 이 매개 변수를 사용합니다. 자세한 내용은 [필드 및 행 종결자 지정&#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)을 참조하세요.  
  
 bcp.exe 명령에서 16진수 표기법으로 행 종료 문자를 지정하는 경우 값은 0x00에서 잘립니다. 예를 들어 0x410041을 지정하면 0x41이 사용됩니다.  
  
 *row_term* 이 하이픈(-) 또는 슬래시(/)로 시작하는 경우에는 **-r** 과 *row_term* 값 사이에 공백을 포함하지 마세요.  
  
 **-R**  
 클라이언트 컴퓨터의 로캘 설정에 정의된 국가별 형식을 사용하여 통화, 날짜 및 시간 데이터를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로 대량 복사하도록 지정합니다. 기본적으로 국가별 설정은 무시됩니다.  
  
 **-S** _server_name_[ **\\** _instance_name_]  
 연결할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 지정합니다. 서버를 지정하지 않으면 **bcp** 유틸리티가 로컬 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 기본 인스턴스에 연결됩니다. 네트워크의 원격 컴퓨터나 명명된 로컬 인스턴스에서 **bcp** 명령을 실행할 때 이 옵션을 지정해야 합니다. 서버에 있는 기본 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결하려면 *server_name*만 지정합니다. 의 명명 된 인스턴스에 연결 하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] *server_name **_\\_** instance_name*를 지정 합니다.  
  
 `-t`*field_term*  
 필드 종결자를 지정합니다. 기본값은 **\t** (탭 문자)입니다. 기본 필드 종결자를 재정의하려면 이 매개 변수를 사용합니다. 자세한 내용은 [필드 및 행 종결자 지정&#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)을 참조하세요.  
  
 bcp.exe 명령에서 16진수 표기법으로 필드 종결자를 지정하는 경우 값은 0x00에서 잘립니다. 예를 들어 0x410041을 지정하면 0x41이 사용됩니다.  
  
 *Field_term* 하이픈 (-) 또는 슬래시 (/)로 시작 하는 경우 `-t` 와 *field_term* 값 사이에 공백을 포함 하지 마십시오.  
  
 **-T**  
 **bcp** 유틸리티가 통합 보안을 사용하는 트러스트된 연결을 통해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로 연결되도록 지정합니다. 네트워크 사용자의 보안 자격 증명, *login_id*및 *password* 는 필요하지 않습니다. **-T** 를 지정하지 않은 경우 성공적으로 로그인하려면 **-U** 와 **-P** 를 지정해야 합니다.  
  
 **-U** _login_id_  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]연결에 사용하는 로그인 ID를 지정합니다.  
  
> [!IMPORTANT]  
>  **bcp** 유틸리티에서 통합 보안을 사용하는 트러스트된 연결을 통해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 연결하는 경우 **사용자 이름** 과 *암호* 를 조합하여 사용하는 대신 *-T* 옵션(트러스트된 연결)을 사용합니다.  
  
 **-v**  
 **bcp** 유틸리티 버전 번호 및 저작권을 보고합니다.  
  
 **-V** (**80** | **90** | **100**| **110**)  
 이전 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전의 데이터 형식을 사용하여 대량 복사 작업을 수행합니다. 이 옵션은 각 필드에 대한 정보를 요청하지 않으며 기본값을 사용합니다.  
  
 **80** = [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]  
  
 **90** = [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
  
 **110 =[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]**  
  
 예를 들어 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]에서는 지원되지 않지만 그 이후 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에 도입된 형식에 대한 데이터를 생성하려면 -V80 옵션을 사용하십시오.  
  
 자세한 내용은 [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)를 참조하세요.  
  
 `-w`  
 유니코드 문자를 사용하여 대량 복사 작업을 수행합니다. 이 옵션은 각 필드에 대해 묻지 않습니다. `nchar`저장소 유형, 접두사, **\t** (탭 문자)를 필드 구분 기호로 사용 하 고 **\n** (줄 바꿈 문자)를 행 종결자로 사용 합니다. `-w`는 `-c`와 호환되지 않습니다.  
  
 자세한 내용은 [유니코드 문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)를 참조하세요.  
  
 **-x**  
 **format** 및 **-f**_format_file_ 옵션과 함께 사용되며 기본 비 XML 서식 파일 대신 XML 기반 서식 파일을 생성합니다. 데이터를 가져오거나 내보낼 때 **-x** 는 작동하지 않습니다. **format** 및 **-f**_format_file_을 함께 사용하지 않으면 오류가 생성됩니다.  
  
## <a name="remarks"></a>설명  
 도구를 설치 하면 **bcp** 12.0 클라이언트가 설치 됩니다 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] . [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]와 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 둘 다에 대해 도구를 설치하면 PATH 환경 변수의 값에 따라 **bcp** 12.0 클라이언트 대신 이전 **bcp** 클라이언트를 사용할 수 있습니다. 이 환경 변수는 실행 파일을 검색하기 위해 Windows에서 사용하는 디렉터리 집합을 정의합니다. 사용 중인 버전을 확인하려면 Windows 명령 프롬프트에서 **bcp /v** 명령을 실행합니다. PATH 환경 변수에서 명령 경로를 설정하는 방법은 Windows 도움말을 참조하십시오.  
  
 XML 서식 파일은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 도구를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client와 함께 설치한 경우에만 지원됩니다.  
  
 **bcp** 유틸리티의 위치 또는 실행 방법과 명령 프롬프트 유틸리티 구문 표기 규칙에 대한 자세한 내용은 [명령 프롬프트 유틸리티 참조&#40;데이터베이스 엔진#41;](../tools/command-prompt-utility-reference-database-engine.md)를 참조하세요.  
  
 대량 가져오기 또는 내보내기 작업을 위해 데이터를 준비하는 방법은 [대량 내보내기 또는 가져오기를 위한 데이터 준비&#40;SQL Server&#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)에 대한 지식이 필요하지 않습니다.  
  
 대량 가져오기로 수행된 행 삽입 작업이 트랜잭션 로그에 기록되는 경우에 대한 자세한 내용은 [대량 가져오기의 최소 로깅을 위한 선행 조건](../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)을 참조하세요.  
  
## <a name="native-data-file-support"></a>네이티브 데이터 파일 지원  
 In [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에서 **bcp** 유틸리티는 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]및 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]와 호환되는 네이티브 데이터 파일만 지원합니다.  
  
## <a name="computed-columns-and-timestamp-columns"></a>계산 열 및 타임스탬프 열  
 가져올 데이터 파일에 있는 계산 열 또는 `timestamp` 열의 값은 무시되며 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 자동으로 이 값을 할당합니다. 데이터 파일의 테이블에 계산 열 또는 `timestamp` 열의 값이 없으면 데이터를 가져올 때 서식 파일을 사용하여 테이블에 있는 계산 열 또는 `timestamp` 열을 건너뛰도록 지정합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 해당 열에 자동으로 값을 할당합니다.  
  
 계산 열 및 `timestamp` 열은 보통 때와 같이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 데이터 파일로 대량 복사됩니다.  
  
## <a name="specifying-identifiers-that-contain-spaces-or-quotation-marks"></a>공백 또는 따옴표를 포함하는 식별자 지정  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 식별자에 중간 공백이나 따옴표와 같은 문자가 포함될 수 있습니다. 이러한 식별자는 다음과 같이 처리해야 합니다.  
  
-   명령 프롬프트에서 공백 또는 따옴표가 포함된 식별자나 파일 이름을 지정할 때는 식별자를 큰따옴표("")로 묶습니다.  
  
     예를 들어 다음 `bcp out` 명령은 `Currency Types.dat`라는 데이터 파일을 만듭니다.  
  
    ```  
    bcp AdventureWorks2012.Sales.Currency out "Currency Types.dat" -T -c  
    ```  
  
-   공백 또는 따옴표를 포함하는 데이터베이스 이름을 지정하려면 `-q` 옵션을 사용해야 합니다.  
  
-   중간 공백이나 따옴표가 포함된 소유자, 테이블 또는 뷰 이름을 지정하려면 다음 중 하나를 수행합니다.  
  
    -   `-q` 옵션을 지정합니다. 또는  
  
    -   따옴표 안에서 소유자, 테이블 또는 뷰 이름을 대괄호([])로 묶습니다.  
  
## <a name="data-validation"></a>데이터 유효성 검사  
 **bcp** 는 이제 데이터 유효성 검사 및 데이터 검사를 강제로 실행하므로 스크립트를 데이터 파일의 잘못된 데이터에 대해 실행할 경우 오류가 발생할 수 있습니다. 예를 들어 **bcp** 는 이제 다음을 확인합니다.  
  
-   `float` 또는 `real` 데이터 형식의 네이티브 표시가 유효한지 여부  
  
-   유니코드 데이터의 길이가 짝수 바이트인지 여부  
  
 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 대량으로 가져올 수 있었던 잘못된 데이터 형식은 이제 로드되지 않습니다. 이전 버전에서는 클라이언트가 잘못된 데이터에 액세스해야 오류가 발생했습니다. 추가 유효성 검사를 수행하면 대량 로드 이후 데이터를 쿼리할 때 발생할 수 있는 예상치 못한 문제가 최소화됩니다.  
  
## <a name="bulk-exporting-or-importing-sqlxml-documents"></a>SQLXML 문서 대량 내보내기 또는 가져오기  
 SQLXML 데이터를 대량으로 내보내거나 가져오려면 서식 파일에서 다음 데이터 형식 중 하나를 사용합니다.  
  
|데이터 형식|영향|  
|---------------|------------|  
|SQLCHAR 또는 SQLVARYCHAR|데이터를 클라이언트 코드 페이지나 데이터 정렬에 포함된 코드 페이지로 보냅니다. 이는 서식 파일을 지정하지 않고 `-c` 스위치를 지정하는 것과 효과가 동일합니다.|  
|SQLNCHAR 또는 SQLNVARCHAR|데이터를 유니코드로 보냅니다. 이는 서식 파일을 지정하지 않고 `-w` 스위치를 지정하는 것과 효과가 동일합니다.|  
|SQLBINARY 또는 SQLVARYBIN|데이터를 변환하지 않고 보냅니다.|  
  
## <a name="permissions"></a>사용 권한  
 **bcpout** 작업을 수행하려면 원본 테이블에 대한 SELECT 권한이 있어야 합니다.  
  
 **bcpin** 작업을 수행하려면 적어도 대상 테이블에 대한 SELECT/INSERT 권한이 있어야 합니다. 또한 다음과 같은 경우 ALTER TABLE 권한이 있어야 합니다.  
  
-   제약 조건이 있으며 CHECK_CONSTRAINTS 힌트가 지정되지 않았습니다.  
  
    > [!NOTE]  
    >  기본적으로 제약 조건은 사용되지 않습니다. 제약 조건을 명시적으로 사용하려면 CHECK_CONSTRAINTS 힌트와 함께 **-h** 옵션을 사용합니다.  
  
-   트리거가 있으며 FIRE_TRIGGER 힌트가 지정되지 않았습니다.  
  
    > [!NOTE]  
    >  기본적으로 트리거는 실행되지 않습니다. 트리거를 명시적으로 실행하려면 FIRE_TRIGGERS 힌트와 함께 **-h** 옵션을 사용합니다.  
  
-   **-E** 옵션을 사용하여 데이터 파일에서 ID 값을 가져옵니다.  
  
> [!NOTE]  
>  대상 테이블에 대해 ALTER TABLE 권한이 필요하게 된 것은 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]부터였습니다. 이 요구 사항으로 인해 사용자 계정에 대상 테이블에 대한 ALTER 테이블 권한이 없을 경우 트리거 및 제약 조건 검사를 실행하지 않는 **bcp** 스크립트가 실패할 수 있습니다.  
  
## <a name="character-mode--c-and-native-mode--n-best-practices"></a>문자 모드(-c) 및 기본 모드(-n) 최선의 구현 방법  
 이 섹션에는 문자 모드(-c) 및 기본 모드(-n) 사용 시의 권장 사항이 나와 있습니다.  
  
-   (관리자/사용자) 가능하면 구분 기호 문제를 방지하기 위해 기본 모드(-n)를 사용하십시오. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 사용하여 내보내기 및 가져오기를 수행하려면 기본 형식을 사용합니다. 데이터를 비 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스로 가져오려는 경우에는 -c 또는 -w 옵션을 사용하여[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 데이터를 내보냅니다.  
  
-   (관리자) BCP OUT를 사용할 때는 데이터를 확인합니다. 예를 들어 BCP OUT, BCP IN, BCP OUT을 차례로 사용하는 경우에는 데이터가 정상적으로 내보내기되었으며 몇몇 데이터 값의 일부분으로 종결자 값이 사용되지 않았는지 확인해야 합니다. 종결자 값과 데이터 값 간의 충돌을 방지하려면 임의의 16진수 값을 사용하여 기본 종결자를 무시할 수 있습니다(-t 및 -r 옵션 사용).  
  
-   (사용자) 실제 문자열 값 간의 충돌 가능성을 최소화하려면 길고 고유한 종결자(바이트 또는 문자 시퀀스)를 사용합니다. 이렇게 하려면 -t 및 -r 옵션을 사용하면 됩니다.  
  
## <a name="examples"></a>예  
 이 섹션에는 다음 예제가 포함되어 있습니다.  
  
-   A. 데이터 파일로 테이블 행 복사(트러스트된 연결 사용)  
  
-   B. 데이터 파일로 테이블 행 복사(혼합 모드 인증 사용)  
  
-   C. 파일에서 테이블로 데이터 복사  
  
-   D. 데이터 파일로 특정 열 복사  
  
-   E. 데이터 파일로 특정 행 복사  
  
-   F. 쿼리에서 데이터 파일로 데이터 복사  
  
-   G. 비 XML 서식 파일 만들기  
  
-   H. XML 서식 파일 만들기  
  
-   9\. **bcp**에서 서식 파일을 사용하여 대량 가져오기 수행  
  
### <a name="a-copying-table-rows-into-a-data-file-with-a-trusted-connection"></a>A. 데이터 파일로 테이블 행 복사(트러스트된 연결 사용)  
 다음 예에서는 **테이블의** out `AdventureWorks2012.Sales.Currency` 옵션에 대해 설명합니다. 이 예에서는 `Currency.dat`라는 데이터 파일을 만들고 문자 형식을 사용하여 테이블 데이터를 파일에 복사합니다. 이 예에서는 Windows 인증을 사용하고 있고 **bcp** 명령을 실행 중인 서버 인스턴스에 트러스트된 연결이 설정되어 있다고 가정합니다.  
  
 명령 프롬프트에서 다음 명령을 입력합니다.  
  
```  
bcp AdventureWorks2012.Sales.Currency out Currency.dat -T -c  
```  
  
### <a name="b-copying-table-rows-into-a-data-file-with-mixed-mode-authentication"></a>B. 데이터 파일로 테이블 행 복사(혼합 모드 인증 사용)  
 다음 예에서는 **테이블의** out `AdventureWorks2012.Sales.Currency` 옵션에 대해 설명합니다. 이 예에서는 `Currency.dat`라는 데이터 파일을 만들고 문자 형식을 사용하여 테이블 데이터를 파일에 복사합니다.  
  
 이 예에서는 혼합 모드 인증을 사용하고 있다고 가정합니다. **-U** 스위치를 사용하여 로그인 ID를 지정해야 합니다. 또한 로컬 컴퓨터에 있는 기본 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결하지 않는 한 **-S** 스위치를 사용하여 시스템 이름을 지정하고 원하는 경우 인스턴스 이름을 지정합니다.  
  
```  
bcp AdventureWorks2012.Sales.Currency out Currency.dat -c -U<login_id> -S<server_name\instance_name>  
```  
  
 시스템에서 암호를 묻는 메시지를 표시합니다.  
  
### <a name="c-copying-data-from-a-file-to-a-table"></a>C. 파일에서 테이블로 데이터 복사  
 다음 예에서는 앞의 예에서 만든 `Currency.dat` 파일을 사용하여 **in** 옵션에 대해 설명합니다. 그러나 먼저 이 예에서는 데이터를 복사해 넣을 빈 `AdventureWorks2012 Sales.Currency` 테이블 복사본 `Sales.Currency2`를 만듭니다. 이 예에서는 Windows 인증을 사용하고 있고 **bcp** 명령을 실행 중인 서버 인스턴스에 트러스트된 연결이 설정되어 있다고 가정합니다.  
  
 빈 테이블을 만들려면 쿼리 편집기에서 다음 명령을 입력합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * INTO AdventureWorks2012.Sales.Currency2   
FROM AdventureWorks2012.Sales.Currency WHERE 1=2;  
```  
  
 문자 데이터를 새 테이블로 대량 복사하려면 즉, 데이터를 가져오려면 명령 프롬프트에서 다음 명령을 입력합니다.  
  
```  
bcp AdventureWorks2012.Sales.Currency2 in Currency.dat -T -c  
```  
  
 명령이 성공적으로 실행되었는지 확인하려면 쿼리 편집기에서 테이블 내용을 표시하고 다음을 입력합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM Sales.Currency2  
```  
  
### <a name="d-copying-a-specific-column-into-a-data-file"></a>D. 데이터 파일로 특정 열 복사  
 특정 열을 복사하려면 **queryout** 옵션을 사용합니다. 다음 예에서는 `Name` 테이블의 `Sales.Currency` 열만 데이터 파일로 복사합니다. 이 예에서는 Windows 인증을 사용하고 있고 **bcp** 명령을 실행 중인 서버 인스턴스에 트러스트된 연결이 설정되어 있다고 가정합니다.  
  
 Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
bcp "SELECT Name FROM AdventureWorks.Sales.Currency" queryout Currency.Name.dat -T -c  
```  
  
### <a name="e-copying-a-specific-row-into-a-data-file"></a>E. 데이터 파일로 특정 행 복사  
 특정 행을 복사하려면 **queryout** 옵션을 사용합니다. 다음 예에서는 `Jarrod Rana`라는 연락처 행만 `AdventureWorks2012.Person.Person` 테이블에서 데이터 파일(`Jarrod Rana.dat`)로 복사합니다. 이 예에서는 Windows 인증을 사용하고 있고 **bcp** 명령을 실행 중인 서버 인스턴스에 트러스트된 연결이 설정되어 있다고 가정합니다.  
  
 Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
bcp "SELECT * FROM AdventureWorks2012.Person.Person WHERE FirstName='Jarrod' AND LastName='Rana' "  queryout "Jarrod Rana.dat" -T -c  
```  
  
### <a name="f-copying-data-from-a-query-to-a-data-file"></a>F. 쿼리에서 데이터 파일로 데이터 복사  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 문의 결과 집합을 데이터 파일로 복사하려면 **queryout** 옵션을 사용합니다. 다음 예에서는 `AdventureWorks2012.Person.Person` 테이블에서 성과 이름을 기준으로 정렬된 이름을 `Contacts.txt` 데이터 파일로 복사합니다. 이 예에서는 Windows 인증을 사용하고 있고 **bcp** 명령을 실행 중인 서버 인스턴스에 트러스트된 연결이 설정되어 있다고 가정합니다.  
  
 Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
bcp "SELECT FirstName, LastName FROM AdventureWorks2012.Person.Person ORDER BY LastName, Firstname" queryout Contacts.txt -c -T  
```  
  
### <a name="g-creating-a-non-xml-format-file"></a>G. 비 XML 서식 파일 만들기  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스의 `Currency.fmt` 테이블에 대해 `Sales.Currency`라는 비 XML 서식 파일을 만듭니다. 이 예에서는 Windows 인증을 사용하고 있고 **bcp** 명령을 실행 중인 서버 인스턴스에 트러스트된 연결이 설정되어 있다고 가정합니다.  
  
 Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
bcp AdventureWorks2012.Sales.Currency format nul -T -c  -f Currency.fmt  
```  
  
 자세한 내용은 [비 XML 서식 파일&#40;SQL Server&#41;](../relational-databases/import-export/xml-format-files-sql-server.md)에서 원래 지원했던 서식 파일입니다.  
  
### <a name="h-creating-an-xml-format-file"></a>H. XML 서식 파일 만들기  
 다음 예에서는 `Currency.xml` 데이터베이스의 `Sales.Currency` 테이블에 대해 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 이라는 XML 서식 파일을 만듭니다. 이 예에서는 Windows 인증을 사용하고 있고 **bcp** 명령을 실행 중인 서버 인스턴스에 트러스트된 연결이 설정되어 있다고 가정합니다.  
  
 Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
bcp AdventureWorks2012.Sales.Currency format nul -T -c -x -f Currency.xml  
```  
  
> [!NOTE]  
>  **-x** 스위치를 사용하려면 **bcp** 9.0 클라이언트를 사용해야 합니다. **Bcp** 9.0 클라이언트를 사용 하는 방법에 대 한 자세한 내용은 "주의"를 참조 하십시오.  
  
 자세한 내용은 [XML 서식 파일&#40;SQL Server&#41;](../relational-databases/import-export/xml-format-files-sql-server.md)의 두 가지 서식 파일 유형을 대량으로 내보내고 가져올 수 있습니다.  
  
### <a name="i-using-a-format-file-to-bulk-import-with-bcp"></a>9\. bcp에서 서식 파일을 사용하여 대량 가져오기 수행  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스로 데이터를 가져올 때 이전에 만든 서식 파일을 사용하려면 **in** 옵션과 함께 **-f** 스위치를 사용합니다. 예를 들어 다음 명령은 이전에 만든 서식 파일인 `Currency.dat`을 사용하여 데이터 파일 `Sales.Currency`의 내용을 `Sales.Currency2` 테이블의 복사본인 `Currency.xml`로 대량 복사합니다. 이 예에서는 Windows 인증을 사용하고 있고 **bcp** 명령을 실행 중인 서버 인스턴스에 트러스트된 연결이 설정되어 있다고 가정합니다.  
  
 Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
bcp AdventureWorks2012.Sales.Currency2 in Currency.dat -T -f Currency.xml  
```  
  
> [!NOTE]  
>  데이터 파일 필드와 테이블 열의 숫자, 순서, 데이터 형식 등이 다른 경우 서식 파일을 사용하면 유용합니다. 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)를 참조하세요.  
  
## <a name="additional-examples"></a>추가 예  
 다음 항목에는 **bcp**를 사용 하는 예가 포함 되어 있습니다.  
  
-   [서식 파일 만들기&#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
-   [XML 문서 대량 가져오기 및 내보내기 예제&#40;SQL Server&#41;](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [데이터 대량 가져오기 중 ID 값 유지&#40;SQL Server&#41;](../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [필드 및 행 종결자 지정&#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [대량 내보내기 또는 가져오기를 위한 데이터 준비 &#40;SQL Server&#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Transact-sql&#41;&#40;QUOTED_IDENTIFIER 설정](/sql/t-sql/statements/set-quoted-identifier-transact-sql)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [Transact-sql&#41;sp_tableoption &#40;](/sql/relational-databases/system-stored-procedures/sp-tableoption-transact-sql)   
 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)  
  
  
