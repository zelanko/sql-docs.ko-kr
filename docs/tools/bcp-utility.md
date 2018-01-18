---
title: "bcp 유틸리티 | Microsoft Docs"
ms.custom: 
ms.date: 09/26/2016
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: bcp
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "222"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1598d16877f42d0aef9f4a997e47492bd3fee1c7
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="bcp-utility"></a>bcp 유틸리티
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

 > 이전 버전의 SQL Server와 관련 된 콘텐츠를 참조 하십시오. [bcp 유틸리티](https://msdn.microsoft.com/en-US/library/ms162802(SQL.120).aspx)합니다.


  **대**량 **복**사 **프**프로그램 유틸리티(**bcp**)는 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스와 사용자가 지정한 형식의 데이터 파일 간에 데이터를 대량 복사합니다. **bcp** 유틸리티를 사용하여 많은 수의 새 행을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 테이블로 가져오거나 테이블에서 데이터 파일로 데이터를 내보낼 수 있습니다. **queryout** 옵션과 함께 사용하는 경우를 제외하고 이 유틸리티를 사용하는 데에는 [!INCLUDE[tsql](../includes/tsql-md.md)]에 대한 지식이 필요하지 않습니다. 테이블로 데이터를 가져오려면 해당 테이블에 대해 만든 서식 파일을 사용하거나 이 테이블의 열에 적합한 테이블 구조와 데이터 형식을 알아야 합니다.  
  
 ![항목 링크 아이콘](../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") 에 사용 되는 구문 표기 규칙에 대 한는 **bcp** 구문 참조 [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41; ](../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
> [!NOTE]
> **bcp** 를 사용하여 데이터를 백업하는 경우 서식 파일을 만들어 데이터 서식을 기록합니다. **bcp** 데이터 파일에는 스키마 또는 서식 정보가 **포함되어 있지 않기** 때문에 테이블이나 뷰가 삭제된 경우 서식 파일이 없으면 데이터를 가져오지 못할 수 있습니다.  
  
<table><th>구문</th><tr><td><pre>
bcp [<a href="#db_name">database_name.</a>] <a href="#schema">schema</a>.{<a href="#tbl_name">table_name</a> | <a href="#vw_name">view_name</a> | <a href="#query">"query"</a>
    {<a href="#in">in</a> <a href="#data_file">data_file</a> | <a href="#out">out</a> <a href="#data_file">data_file</a> | <a href="#qry_out">queryout</a> <a href="#data_file">data_file</a> | <a href="#format">format</a> <a href="#format">nul</a>}
<a>                                                                                                         </a>
    [<a href="#a">-a packet_size</a>]
    [<a href="#b">-b batch_size</a>]
    [<a href="#c">-c</a>]
    [<a href="#C">-C { ACP | OEM | RAW | code_page } </a>]
    [<a href="#d">-d database_name</a>]
    [<a href="#e">-e err_file</a>]
    [<a href="#E">-E</a>]
    [<a href="#f">-f format_file</a>]
    [<a href="#F">-F first_row</a>]
    [<a href="#h">-h"hint [,...n]"</a>]
    [<a href="#i">-i input_file</a>]
    [<a href="#k">-k</a>]
    [<a href="#K">-K application_intent</a>]
    [<a href="#L">-L last_row</a>]
    [<a href="#m">-m max_errors</a>]
    [<a href="#n">-n</a>]
    [<a href="#N">-N</a>]
    [<a href="#o">-o output_file</a>]
    [<a href="#P">-P password</a>]
    [<a href="#q">-q</a>]
    [<a href="#r">-r row_term</a>]
    [<a href="#R">-R</a>]
    [<a href="#S">-S [server_name[\instance_name]</a>]
    [<a href="#t">-t field_term</a>]
    [<a href="#T">-T</a>]
    [<a href="#U">-U login_id</a>]
    [<a href="#v">-v</a>]
    [<a href="#V">-V (80 | 90 | 100 | 110 | 120 | 130 ) </a>]
    [<a href="#w">-w</a>]
    [<a href="#x">-x</a>]
</pre></td></tr></table>  
  
## <a name="arguments"></a>인수  
 ***data_file***<a name="data_file"></a>  
 데이터 파일의 전체 경로입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 데이터를 대량으로 가져오는 경우 데이터 파일에는 지정한 테이블 또는 뷰로 복사할 데이터가 포함됩니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 데이터를 대량으로 내보내는 경우 데이터 파일에는 테이블 또는 뷰에서 복사한 데이터가 포함됩니다. 데이터 파일 경로는 1에서 255자까지 포함할 수 있습니다. 데이터 파일에는 최대 2^63 - 1개의 행이 포함될 수 있습니다.  
  
 ***database_name***<a name="db_name"></a>  
 지정한 테이블 또는 뷰가 있는 데이터베이스의 이름입니다. 이 인수를 지정하지 않으면 사용자의 기본 데이터베이스를 사용합니다.  
  
 **d-**를 사용하여 데이터베이스 이름을 명시적으로 지정할 수도 있습니다.  
  
 **in** *data_file* | **out** *data_file* | **queryout** *data_file* | **format nul**  
 다음과 같이 대량 복사 방향을 지정합니다.  
  
-   **in**<a name="in"></a> 은 파일에서 데이터베이스 테이블 또는 뷰로 복사합니다.  
  
-   **out**<a name="out"></a> 은 데이터베이스 테이블 또는 뷰에서 파일로 복사합니다. 기존 파일을 지정하면 이 파일을 덮어씁니다. 데이터를 추출할 때 **bcp** 유틸리티는 빈 문자열을 null로 나타내고 null 문자열은 빈 문자열로 나타냅니다.  
  
-   **queryout**<a name="qry_out"></a> 은 쿼리에서 복사하며 쿼리에서 데이터를 대량 복사하는 경우에만 지정해야 합니다.  
  
-   **format**<a name="format"></a> 은**-n**, **-c**, **-w**, **-N**등의 지정된 옵션과 테이블 또는 뷰 구분 기호를 기준으로 서식 파일을 만듭니다. 데이터를 대량 복사하는 경우 **bcp** 명령은 서식 파일을 참조할 수 있으므로 대화형으로 서식 정보를 다시 입력할 필요가 없습니다. **format** 옵션에는 **-f** 옵션이 필요하며 XML 서식 파일을 만드는 경우 **-x** 옵션도 필요합니다. 자세한 내용은 [서식 파일 만들기&#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md)를 참조하세요. **nul** 을 값으로 지정해야 합니다(**format nul**).  
  
 ***owner***<a name="schema"></a>  
 테이블 또는 뷰의 소유자 이름입니다. 작업을 수행하는 사용자가 지정한 테이블 또는 뷰를 소유하고 있는 경우에는*owner* 를 생략할 수 있습니다. *owner*를 지정하지 않은 경우 작업을 수행하는 사용자가 지정한 테이블이나 뷰의 소유자가 아니면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 오류 메시지를 반환하고 작업이 취소됩니다.  
  
**"** ***query*** **"**<a name="query"></a> Is a [!INCLUDE[tsql](../includes/tsql-md.md)] query that returns a result set. 쿼리에서 여러 결과 집합을 반환하는 경우 첫 번째 결과 집합만 데이터 파일에 복사되고 그 다음 결과 집합은 무시됩니다. 쿼리는 큰따옴표로 묶고 쿼리 안에 포함되는 모든 것은 작은따옴표로 묶습니다. 쿼리에서 데이터를 대량 복사할 때는**queryout** 도 지정해야 합니다.  
  
 쿼리는 bcp 문을 실행하기 전에 저장 프로시저 내에서 참조되는 모든 테이블이 존재하는 한 저장 프로시저를 참조할 수 있습니다. 예를 들어 저장 프로시저가 임시 테이블을 생성하면 이 임시 테이블을 런타임에만 사용할 수 있고 문 실행 시에는 사용할 수 없기 때문에 **bcp** 문이 실패합니다. 이 경우 테이블에 저장 프로시저 결과를 삽입한 다음 **bcp** 를 사용하여 테이블에서 데이터 파일로 데이터를 복사할 수 있습니다.  
  
 ***table_name***<a name="tbl_name"></a>  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로 데이터를 가져올 때(**in**)는 대상 테이블의 이름이고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 데이터를 내보낼 때(**out**)는 원본 테이블의 이름입니다.  
  
 ***view_name***<a name="vw_name"></a>   
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로 데이터를 복사할 때(**in**)는 대상 뷰의 이름이고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 데이터를 복사할 때(**out**)는 원본 뷰의 이름입니다. 모든 열이 같은 테이블을 참조하는 뷰만 대상 뷰로 사용할 수 있습니다. 뷰에 데이터를 복사하는 경우의 제한 사항에 대한 자세한 내용은 [INSERT&#40;Transact-SQL&#41;](../t-sql/statements/insert-transact-sql.md)를 참조하세요.  
  
 **-a** ***packet_size***<a name="a"></a>  
 서버에서 전송되거나 서버로 전송되는 네트워크 패킷당 바이트 수를 지정합니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 또는 **sp_configure** 시스템 저장 프로시저를 사용하여 서버 구성 옵션을 설정할 수 있습니다. 그러나 이 옵션을 사용하여 서버 구성 옵션을 개별적으로 재정의할 수 있습니다. *packet_size* 는 4096 ~ 65535바이트일 수 있고 기본값은 4096입니다.  
  
 패킷 크기가 커지면 대량 복사 작업의 성능이 향상될 수 있습니다. 더 큰 패킷을 요청했는데 허용되지 않으면 기본값이 사용됩니다. **bcp** 유틸리티가 생성하는 성능 통계에는 사용되는 패킷의 크기가 나타납니다.  
  
 **-b** ***batch_size***<a name="b"></a>  
 가져온 데이터의 일괄 처리당 행 수를 지정합니다. 각 일괄 처리는 커밋되기 전에 전체 일괄 처리를 가져오는 별도의 트랜잭션으로 가져오고 기록합니다. 기본적으로 데이터 파일의 모든 행은 하나의 일괄 처리로 가져옵니다. 여러 일괄 처리에 행을 분산시키려면 데이터 파일의 행 수보다 작은 *batch_size* 를 지정합니다. 일괄 처리에 대한 트랜잭션이 실패하면 현재 일괄 처리에서 삽입한 내용만 롤백됩니다. 커밋된 트랜잭션으로 이미 가져온 일괄 처리는 나중에 발생한 오류의 영향을 받지 않습니다.  
  
 와 함께에서이 옵션을 사용 하지 않으면는 **-h "**ROWS_PER_BATCH  **= ***bb***"** 옵션입니다.  
 
 **-c**<a name="c"></a>  
 문자 데이터 형식을 사용하여 작업을 수행합니다. 이 옵션은 각 필드에 대한 정보를 요청하지 않습니다. 이 옵션은 **char** 을 저장소 유형으로 사용하고 접두사를 사용하지 않으며 **\t** (탭 문자)를 필드 구분 기호로 사용하고 **\r\n** (줄 바꿈 문자)을 행 종결자로 사용합니다. **-c**는 **-w**와 호환되지 않습니다.  
  
 자세한 내용은 [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)를 참조하세요.  
  
 **-C** { **ACP** | **OEM** | **RAW** | *code_page* }<a name="C"></a>   
 데이터 파일에서 데이터의 코드 페이지를 지정합니다. *code_page* 는 문자 값이 127보다 크거나 32보다 작은 **char**, **varchar**또는 **text** 열이 데이터에 포함된 경우에만 적합합니다.  
  
> [!NOTE]
> 데이터 정렬/코드 페이지 사양보다 65001 옵션에 더 높은 우선 순위를 두려는 경우를 제외하고는 서식 파일의 각 열에 대한 데이터 정렬 이름을 지정하는 것이 좋습니다.
  
|코드 페이지 값|설명|  
|---------------------|-----------------|  
|ACP|[!INCLUDE[vcpransi](../includes/vcpransi-md.md)]/Microsoft Windows(ISO 1252)입니다.|  
|OEM|클라이언트가 사용하는 기본 코드 페이지입니다. **-C** 를 지정하지 않은 경우 사용되는 기본 코드 페이지입니다.|  
|RAW|코드 페이지 간 변환이 일어나지 않습니다. 변환이 일어나지 않으므로 가장 빠른 옵션입니다.|  
|*code_page*|850과 같은 특정 코드 페이지 번호입니다.<br /><br /> 버전 13([!INCLUDE[ssSQL15](../includes/sssql15-md.md)]) 이전 버전은 코드 페이지 65001(UTF-8 인코딩)을 지원하지 않습니다. 버전 13부터 UTF-8 인코딩을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]이전 버전으로 가져올 수 있습니다.|  
  
 **-d** ***database_name***<a name="d"></a>   
 연결할 데이터베이스를 지정합니다. bcp.exe는 기본적으로 사용자의 기본 데이터베이스에 연결됩니다. 경우 **-d** *database_name* 및 세 부분으로 된 이름을 (*database_name.schema.table*bcp.exe에 첫 번째 매개 변수로 전달 된)을 지정 하기 때문에 오류가 발생 하면 데이터베이스 이름을 두 번 지정할 수 없습니다. 경우 *database_name* 시작 하이픈 (-) 또는 슬래시 (/) 사이 공백의 추가 하지 마십시오 **-d** 및 데이터베이스 이름입니다.  
  
 **-e** ***err_file***<a name="e"></a>  
 **bcp** 유틸리티가 파일에서 데이터베이스로 전송할 수 없는 행을 저장하는 데 사용되는 오류 파일의 전체 경로를 지정합니다. **bcp** 명령의 오류 메시지는 사용자의 워크스테이션에 나타납니다. 이 옵션을 사용하지 않으면 오류 파일이 생성되지 않습니다.  
  
 *err_file* 이 하이픈(-) 또는 슬래시(/)로 시작하는 경우에는 **-e** 와 *err_file* 값 사이에 공백을 포함하지 마세요.  
  
 **-E**<a name="E"></a>   
 가져온 데이터 파일의 ID 값이 ID 열에 사용되도록 지정합니다. **-E**를 지정하지 않으면 가져오는 데이터 파일에 있는 이 열의 ID 값이 무시되고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 테이블을 만들 때 지정한 초기값 및 증가값을 기반으로 고유 값을 자동으로 할당합니다.  
  
 데이터 파일에 테이블이나 뷰의 ID 열 값이 포함되지 않은 경우 서식 파일을 사용하여 데이터를 가져올 때 테이블이나 뷰의 ID 열을 생략하도록 지정합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 해당 열에 자동으로 고유 값을 할당합니다. 자세한 내용은 [DBCC CHECKIDENT&#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)를 참조하세요.  
  
 **-E** 옵션을 사용하려면 특별한 권한이 있어야 합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "[주의](#remarks)"를 참조하세요.  
   
 **-f** ***format_file***<a name="f"></a>  
 서식 파일의 전체 경로를 지정합니다. 다음과 같이 이 옵션의 의미는 해당 환경에 따라 다릅니다.  
  
-   **format** 옵션과 함께 **-f** 를 사용하는 경우 지정한 테이블 또는 뷰에 대해 지정한 *format_file* 이 만들어집니다. XML 서식 파일을 만들려면 **-x** 옵션도 지정합니다. 자세한 내용은 [서식 파일 만들기&#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md)를 참조하세요.  
  
-   **-f**를 **in** 또는 **out** 옵션과 함께 사용하는 경우 기존 서식 파일이 필요합니다.  
  
    > [!NOTE]
    > 원할 경우 **in** 또는 **out** 옵션과 함께 서식 파일을 사용할 수도 있습니다. 없는 경우에는 **-f** 옵션, 경우  **-n** , **-c**, **-w**, 또는 **-N** 을 지정 하지 않으면 명령 형식 정보를 묻는 메시지가 표시 되며 응답 내용을 서식 파일 (의 기본 이름은 bcp.fmt 지만 필요)에 저장할 수 있습니다.
  
 *format_file* 이 하이픈(-) 또는 슬래시(/)로 시작하는 경우에는 **-f** 와 *format_file* 값 사이에 공백을 포함하지 마세요.  
  
 **-F** ***first_row***<a name="F"></a>  
 테이블에서 내보내거나 데이터 파일에서 가져올 첫 번째 행 번호를 지정합니다. 이 매개 변수에는 0보다 크고(>) 총 행 수보다 작거나(<) 같은(=) 값을 지정해야 합니다. 이 매개 변수를 지정하지 않을 경우 기본값은 파일의 첫 번째 행입니다.  
  
 *first_row* 는 최대 2^63-1의 값을 갖는 양의 정수입니다. **-F** *first_row* 는 1부터 시작합니다.  
  
**-h** ***"load hints***[ ,... *n*]**"**<a name="h"></a> 은 데이터를 테이블 또는 뷰로 대량으로 가져올 때 사용할 힌트를 지정합니다.  
  
* **ORDER**(***column*[ASC | DESC] [**,**...*n*]**)**  
데이터 파일에 있는 데이터의 정렬 순서입니다. 가져올 데이터를 테이블의 클러스터형 인덱스(있는 경우)에 따라 정렬하면 대량 가져오기 성능이 향상됩니다. 데이터 파일을 클러스터형 인덱스 키와 다른 순서로 정렬하거나 테이블에 클러스터형 인덱스가 없으면 ORDER 절이 무시됩니다. 지정한 열 이름은 대상 테이블에서 올바른 열 이름이어야 합니다. 기본적으로 **bcp** 는 데이터 파일이 정렬되지 않은 것으로 간주합니다. 대량 가져오기 작업을 최적화하기 위해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서는 가져온 데이터가 정렬되어 있는지도 확인합니다.  
  
* **ROWS_PER_BATCH** **=** ***bb***  
일괄 처리당 데이터 행 수( *bb*)입니다. **-b** 를 지정하지 않은 경우에 사용되며 전체 데이터 파일을 단일 트랜잭션으로 서버에 보냅니다. 서버는 *bb*값에 따라 대량 로드를 최적화합니다. 기본적으로 ROWS_PER_BATCH는 알 수 없습니다.  
  
* **KILOBYTES_PER_BATCH** **=** ***cc***  
일괄 처리당 데이터의 대략적인 KB 단위 크기( *cc*)입니다. 기본적으로 KILOBYTES_PER_BATCH는 알 수 없습니다.  
  
* **TABLOCK**  
대량 로드 작업이 진행되는 동안 대량 업데이트 테이블 수준 잠금이 사용되도록 지정합니다. 그렇지 않으면 행 수준 잠금이 사용됩니다. 대량 복사 작업 중에 잠금을 보유하면 테이블의 잠금 경합이 줄어들기 때문에 이 힌트를 사용하면 성능이 크게 향상됩니다. 테이블에 인덱스가 없고 **TABLOCK** 이 지정되어 있으면 여러 클라이언트가 동시에 테이블을 로드할 수 있습니다. 기본적으로 잠금 동작은 **table lock on bulk load**테이블 옵션에 의해 결정됩니다.  
  
  > [!NOTE]
  > 대상 테이블이 클러스터형 columnstore 인덱스인 경우에는 각 동시 스레드가 인덱스 내의 별도 행 그룹에 할당되고 데이터를 로드하기 때문에 여러 동시 클라이언트에서 로드하는 데 TABLOCK 힌트가 필요 없습니다. 자세한 내용은 columnstore 인덱스 개념 항목을 참조하세요.
  
  **CHECK_CONSTRAINTS**  
  대량 가져오기 작업 중 대상 테이블 또는 뷰의 모든 제약 조건을 검사하도록 지정합니다. CHECK_CONSTRAINTS 힌트를 지정하지 않으면 모든 CHECK 및 FOREIGN KEY 제약 조건이 무시되며 작업 후 테이블의 제약 조건은 트러스트되지 않는 것으로 표시됩니다.  
  
  > [!NOTE]
  > UNIQUE, PRIMARY KEY 및 NOT NULL 제약 조건은 항상 적용됩니다.
  
  어느 시점에서는 전체 테이블의 제약 조건을 확인할 필요가 있습니다. 대량 가져오기 작업을 수행하기 전에 테이블이 비어 있지 않은 경우 제약 조건의 유효성을 다시 검사하는 비용이 증분 데이터에 CHECK 제약 조건을 적용하는 비용을 초과할 수 있습니다. 따라서 일반적으로 증분 대량 가져오기 중에 제약 조건을 검사하도록 설정하는 것이 좋습니다.  
  
  입력 데이터에 제약 조건을 위반하는 행이 포함된 경우에는 제약 조건을 사용하지 않을 수 있습니다(기본 동작). CHECK 제약 조건을 사용하지 않으면 데이터를 가져온 다음 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 사용하여 잘못된 데이터를 제거할 수 있습니다.  
  
  > [!NOTE]
  > **bcp**는 이제 데이터 유효성 검사 및 데이터 검사를 강제로 실행하므로 스크립트를 데이터 파일의 잘못된 데이터에 대해 실행할 경우 오류가 발생할 수 있습니다.
  
  > [!NOTE]
  > **-m** *max_errors* 스위치는 제약 조건 검사에 적용되지 않습니다.
  
* **FIRE_TRIGGERS**  
**in** 인수와 함께 지정하면 대량 복사 작업 중에 대상 테이블에 정의한 삽입 트리거가 실행됩니다. FIRE_TRIGGERS를 지정하지 않으면 삽입 트리거가 실행되지 않습니다. FIRE_TRIGGERS는 **out**, **queryout**및 **format** 인수에 대해 무시됩니다.  
  
 **-i** ***input_file***<a name="i"></a>  
 대화형 모드(**-n**, **-c**, **-w**, **-N** 을 지정하지 않음)를 사용하여 대량 복사를 수행할 때 각 데이터 필드에 대한 명령 프롬프트 질문의 응답이 포함된 응답 파일의 이름을 지정합니다.  
  
 *input_file* 이 하이픈(-) 또는 슬래시(/)로 시작하는 경우에는 **-i** 와 *input_file* 값 사이에 공백을 포함하지 마세요.  
  
 **-k**<a name="k"></a>  
 작업 시 삽입된 열에 기본값이 지정되지 않고 빈 열이 Null 값을 보유하도록 지정합니다. 자세한 내용은 [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)을 참조하세요.  
  
 **-K** ***application_intent***<a name="K"></a>   
 서버에 연결할 때 응용 프로그램 작업 유형을 선언합니다. **ReadOnly**값만 사용할 수 있습니다. **-K**를 지정하지 않으면 bcp 유틸리티가 Always On 가용성 그룹에 있는 보조 복제본에 연결할 수 없습니다. 자세한 내용은 [활성 보조: 읽기 가능한 보조 복제본&#40;Always On 가용성 그룹&#41;](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)개념을 소개합니다.  
  
 **-L** ***last_row***<a name="L"></a>  
 테이블에서 내보내거나 데이터 파일에서 가져올 마지막 행 번호를 지정합니다. 이 매개 변수에는 0보다 크고(>) 마지막 행 번호보다 작거나(<) 같은(=) 값을 지정해야 합니다. 이 매개 변수를 지정하지 않을 경우 기본값은 파일의 마지막 행입니다.  
  
 *last_row* 는 최대 2^63-1의 값을 갖는 양의 정수입니다.  
  
**-m** ***max_errors***<a name="m"></a>  
**bcp** 작업이 취소되는 최대 구문 오류 발생 횟수를 지정합니다. 구문 오류란 대상 데이터 형식으로의 데이터 변환 오류를 나타냅니다. 총 *max_errors* 수에는 제약 조건 위반과 같이 서버에서만 검색할 수 있는 오류는 제외됩니다.  
  
 **bcp** 유틸리티가 복사할 수 없는 행은 무시되며 오류가 하나 발생한 것으로 간주됩니다. 이 옵션을 지정하지 않은 경우의 기본값은 10입니다.  
  
> [!NOTE]
> **-m** 옵션 또한 **money** 또는 **bigint** 데이터 형식 변환에는 적용되지 않습니다.
  
**-n**<a name="n"></a>  
데이터의 네이티브(데이터베이스) 데이터 형식을 사용하여 대량 복사 작업을 수행합니다. 이 옵션이 필드마다 표시되지는 않습니다. 이 옵션은 네이티브 값을 사용합니다.  
  
자세한 내용은 [네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)를 참조하세요.  
  
**-N**<a name="N"></a>  
문자가 아닌 데이터의 경우 데이터의 네이티브(데이터베이스) 데이터 형식을 사용하고 문자 데이터의 경우 유니코드 문자를 사용하여 대량 복사 작업을 수행합니다. 이 옵션은 **-w** 옵션을 사용할 때보다 성능이 높으며 데이터 파일을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 간에 데이터를 전송할 때 사용할 수 있습니다. 이 옵션은 각 필드에 대한 정보를 요청하지 않습니다. ANSI 확장 문자가 들어 있는 데이터를 전송하는 경우 기본 모드의 성능을 활용하려고 할 때 이 옵션을 사용하십시오.  
  
 자세한 내용은 [유니코드 네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)를 참조하세요.  
  
 **-N**과 함께 bcp.exe를 사용하여 동일한 테이블 스키마에 데이터를 내보낸 다음 가져올 경우 유니코드를 지원하지 않는 고정 길이 문자 열(예: **char(10)**)이 있으면 잘림 경고가 표시될 수 있습니다.  
  
 이 경고는 무시해도 됩니다. 사용 하 여이 경고를 해결 하는 한 가지 방법은  **-n**  대신 **-N**합니다.  
  
 **-o** ***output_file***<a name="o"></a>  
 명령 프롬프트에서 리디렉션된 출력을 받는 파일의 이름을 지정합니다.  
  
 *output_file* 이 하이픈(-) 또는 슬래시(/)로 시작하는 경우에는 **-o** 와 *output_file* 값 사이에 공백을 포함하지 마세요.  
  
 **-P** ***password***<a name="P"></a>  
 로그인 ID의 암호를 지정합니다. 이 옵션을 사용하지 않으면 **bcp** 명령을 실행하는 동안 암호를 묻는 메시지가 표시됩니다. 암호를 입력하지 않고 명령 프롬프트의 마지막에 이 옵션을 사용하면 **bcp** 는 기본 암호 NULL을 사용합니다.  
  
> [!IMPORTANT]
> [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]
  
 암호를 마스킹하려면 **-U** 옵션과 함께 **-P** 옵션을 지정하지 마세요. 대신 **-U** 옵션 및 기타 스위치와 함께 **bcp** 를 지정하고( **-P**는 지정하지 않음) Enter 키를 누르면 암호를 묻는 메시지가 표시됩니다. 이 방법을 사용하면 암호 입력 시 암호가 마스킹됩니다.  
  
 *password* 가 하이픈(-) 또는 슬래시(/)로 시작하는 경우에는 **-P** 와 *password* 값 사이에 공백을 포함하지 마세요.  
  
 **-q**<a name="q"></a>  
 **bcp** 유틸리티와 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스 간의 연결에서 SET QUOTED_IDENTIFIERS ON 문을 실행합니다. 이 옵션을 사용하여 공백이나 작은따옴표를 포함하는 데이터베이스, 소유자, 테이블 또는 뷰 이름을 지정합니다. 세 부분으로 구성된 테이블 이름이나 뷰 이름 전체를 큰따옴표("")로 묶습니다.  
  
 공백이나 작은따옴표가 들어 있는 데이터베이스 이름을 지정하려면 **–q** 옵션을 사용해야 합니다.  
  
 **-q** 는 **-d**로 전달된 값에는 적용되지 않습니다.  
  
 자세한 내용은 이 항목의 뒷부분에 나오는 [주의](#remarks)를 참조하세요.  
  
 **-r** ***row_term***<a name="r"></a>  
 행 종결자를 지정합니다. 기본값은  **\n**  (줄 바꿈 문자)입니다. 기본 행 종결자를 재정의하려면 이 매개 변수를 사용합니다. 자세한 내용은 [필드 및 행 종결자 지정&#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)을 참조하세요.  
  
 bcp.exe 명령에서 16진수 표기법으로 행 종료 문자를 지정하는 경우 값은 0x00에서 잘립니다. 예를 들어 0x410041을 지정하면 0x41이 사용됩니다.  
  
 *row_term* 이 하이픈(-) 또는 슬래시(/)로 시작하는 경우에는 **-r** 과 *row_term* 값 사이에 공백을 포함하지 마세요.  
  
 **-R**<a name="R"></a>  
 클라이언트 컴퓨터의 로캘 설정에 정의된 국가별 형식을 사용하여 통화, 날짜 및 시간 데이터를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로 대량 복사하도록 지정합니다. 기본적으로 국가별 설정은 무시됩니다.  
  
 **-S** ***server_name*** [\\***instance_name***]<a name="S"> </a> 의 인스턴스를 지정 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 연결 하는 데에 있습니다. 서버를 지정하지 않으면 **bcp** 유틸리티가 로컬 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 기본 인스턴스에 연결됩니다. 네트워크의 원격 컴퓨터나 명명된 로컬 인스턴스에서 **bcp** 명령을 실행할 때 이 옵션을 지정해야 합니다. 서버에 있는 기본 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결하려면 *server_name*만 지정합니다. 명명 된 인스턴스에 연결 하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], 지정 *server_name***\\***instance_name*합니다.  
  
 **-t** ***field_term***<a name="t"></a>  
 필드 종결자를 지정합니다. 기본값은 **\t** (탭 문자)입니다. 기본 필드 종결자를 재정의하려면 이 매개 변수를 사용합니다. 자세한 내용은 [필드 및 행 종결자 지정&#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)을 참조하세요.  
  
 bcp.exe 명령에서 16진수 표기법으로 필드 종결자를 지정하는 경우 값은 0x00에서 잘립니다. 예를 들어 0x410041을 지정하면 0x41이 사용됩니다.  
  
 *field_term* 이 하이픈(-) 또는 슬래시(/)로 시작하는 경우에는 **-t** 와 *field_term* 값 사이에 공백을 포함하지 마세요.  
  
 **-T**<a name="T"></a>  
 **bcp** 유틸리티가 통합 보안을 사용하는 트러스트된 연결을 통해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로 연결되도록 지정합니다. 네트워크 사용자의 보안 자격 증명, *login_id*및 *password* 는 필요하지 않습니다. **–T** 를 지정하지 않은 경우 성공적으로 로그인하려면 **–U** 와 **–P** 를 지정해야 합니다.
 
> [!IMPORTANT]
> **bcp** 유틸리티에서 통합 보안을 사용하는 트러스트된 연결을 통해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 연결하는 경우 **사용자 이름** 과 *암호* 를 조합하여 사용하는 대신 *-T* 옵션(트러스트된 연결)을 사용합니다. **bcp** 유틸리티가 SQL Database 또는 SQL Data Warehouse에 연결할 때 Windows 인증 또는 Azure Active Directory 인증을 사용이 지원되지 않습니다. **-U** 및 **-P** 옵션을 사용하세요. 
  
 **-P** ***login_id***<a name="U"></a>  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]연결에 사용하는 로그인 ID를 지정합니다.  
  
> [!IMPORTANT]
> **bcp** 유틸리티에서 통합 보안을 사용하는 트러스트된 연결을 통해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 연결하는 경우 *사용자 이름*과 *암호*를 조합하여 사용하는 대신 **-T** 옵션(트러스트된 연결)을 사용합니다. **bcp** 유틸리티가 SQL Database 또는 SQL Data Warehouse에 연결할 때 Windows 인증 또는 Azure Active Directory 인증을 사용이 지원되지 않습니다. **-U** 및 **-P** 옵션을 사용하세요.
  
 **-v**<a name="v"></a>  
 **bcp** 유틸리티 버전 번호 및 저작권을 보고합니다.  
  
 **-V** (**80** | **90** | **100** | **110** | **120** | **130** )<a name="V"></a>  
 이전 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전의 데이터 형식을 사용하여 대량 복사 작업을 수행합니다. 이 옵션은 각 필드에 대한 정보를 요청하지 않으며 기본값을 사용합니다.  
  
 **80** = [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]  
  
 **90** = [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
 예를 들어 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]에서는 지원되지 않지만 그 이후 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에 도입된 형식에 대한 데이터를 생성하려면 -V80 옵션을 사용하십시오.  
  
 자세한 내용은 [SQL Server 이전 버전으로부터 기본 및 문자 형식 데이터 가져오기](../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)를 참조하세요.  
  
 **-w**<a name="w"></a>  
 유니코드 문자를 사용하여 대량 복사 작업을 수행합니다. 이 옵션은 각 필드에 대한 정보를 요청하지 않습니다. 이 옵션은 **nchar** 을 저장소 유형으로 사용하고 접두사를 사용하지 않으며 **\t** (탭 문자)를 필드 구분 기호로 사용하고 **\n** (줄 바꿈 문자)을 행 종결자로 사용합니다. **-w** 는 **-c**와 호환되지 않습니다.  
  
 자세한 내용은 [유니코드 문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)를 참조하세요.  
  
 **-x**<a name="x"></a>  
 **format** 및 **-f** *format_file* 옵션과 함께 사용되며 기본 비 XML 서식 파일 대신 XML 기반 서식 파일을 생성합니다. 데이터를 가져오거나 내보낼 때 **-x** 는 작동하지 않습니다. **format** 및 **-f** *format_file*을 함께 사용하지 않으면 오류가 생성됩니다.  
  
## 주의<a name="remarks"></a>
 총 **bcp** 도구를 설치하면 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 13.0 클라이언트가 설치됩니다. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 와 이전 버전 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]둘 다에 대해 도구가 설치된 경우 PATH 환경 변수의 값에 따라 **bcp** 13.0 클라이언트 대신 이전 **bcp** 클라이언트를 사용하게 될 수 있습니다. 이 환경 변수는 실행 파일을 검색하기 위해 Windows에서 사용하는 디렉터리 집합을 정의합니다. 사용 중인 버전을 확인하려면 Windows 명령 프롬프트에서 **bcp /v** 명령을 실행합니다. PATH 환경 변수에서 명령 경로를 설정하는 방법은 Windows 도움말을 참조하십시오.  
 
bcp 유틸리티는 [Microsoft SQL Server 2016 기능 팩](https://www.microsoft.com/en-us/download/details.aspx?id=52676)에서 별도로 다운로드할 수도 있습니다.  `ENU\x64\MsSqlCmdLnUtils.msi` 또는 `ENU\x86\MsSqlCmdLnUtils.msi`중에 선택합니다.

  
 XML 서식 파일은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 도구를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client와 함께 설치한 경우에만 지원됩니다.  
  
 **bcp** 유틸리티의 위치 또는 실행 방법과 명령 프롬프트 유틸리티 구문 표기 규칙에 대한 자세한 내용은 [명령 프롬프트 유틸리티 참조&#40;데이터베이스 엔진#41;](../tools/command-prompt-utility-reference-database-engine.md)를 참조하세요.  
  
 대량 가져오기 또는 내보내기 작업을 위해 데이터를 준비하는 방법은 [대량 내보내기 또는 가져오기를 위한 데이터 준비&#40;SQL Server&#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)를 참조하세요.  
  
 대량 가져오기로 수행된 행 삽입 작업이 트랜잭션 로그에 기록되는 경우에 대한 자세한 내용은 [대량 가져오기의 최소 로깅을 위한 선행 조건](../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)을 참조하세요.  
  
## <a name="native-data-file-support"></a>네이티브 데이터 파일 지원  
 In [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에서 **bcp** 유틸리티는 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]및 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]와 호환되는 네이티브 데이터 파일만 지원합니다.  
  
## <a name="computed-columns-and-timestamp-columns"></a>계산 열 및 타임스탬프 열  
 가져올 데이터 파일에 있는 계산 열 또는 **timestamp** 열의 값은 무시되며 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 자동으로 이 값을 할당합니다. 데이터 파일의 테이블에 계산 열 또는 **timestamp** 열의 값이 없으면 데이터를 가져올 때 서식 파일을 사용하여 테이블에 있는 계산 열 또는 **timestamp** 열을 건너뛰도록 지정합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서는 해당 열에 자동으로 값을 할당합니다.  
  
 계산 열 및 **timestamp** 열은 보통 때와 같이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 데이터 파일로 대량 복사됩니다.  
  
## <a name="specifying-identifiers-that-contain-spaces-or-quotation-marks"></a>공백 또는 따옴표를 포함하는 식별자 지정  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 식별자에 중간 공백이나 따옴표와 같은 문자가 포함될 수 있습니다. 이러한 식별자는 다음과 같이 처리해야 합니다.  
  
-   명령 프롬프트에서 공백 또는 따옴표가 포함된 식별자나 파일 이름을 지정할 때는 식별자를 큰따옴표("")로 묶습니다.  
  
     예를 들어 다음 `bcp out` 명령은 `Currency Types.dat`라는 데이터 파일을 만듭니다.  
  
    ```  
    bcp AdventureWorks2012.Sales.Currency out "Currency Types.dat" -T -c  
    ```  
  
-   공백 또는 따옴표를 포함하는 데이터베이스 이름을 지정하려면 **-q** 옵션을 사용해야 합니다.  
  
-   중간 공백이나 따옴표가 포함된 소유자, 테이블 또는 뷰 이름을 지정하려면 다음 중 하나를 수행합니다.  
  
    -   **-q** 옵션을 지정합니다. 또는  
  
    -   따옴표 안에서 소유자, 테이블 또는 뷰 이름을 대괄호([])로 묶습니다.  
  
## <a name="data-validation"></a>데이터 유효성 검사  
 **bcp** 는 이제 데이터 유효성 검사 및 데이터 검사를 강제로 실행하므로 스크립트를 데이터 파일의 잘못된 데이터에 대해 실행할 경우 오류가 발생할 수 있습니다. 예를 들어 **bcp** 는 이제 다음을 확인합니다.  
  
-   **float** 또는 **real** 데이터 형식의 네이티브 표시가 유효한지 여부  
  
-   유니코드 데이터의 길이가 짝수 바이트인지 여부  
  
 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 대량으로 가져올 수 있었던 잘못된 데이터 형식은 이제 로드되지 않습니다. 이전 버전에서는 클라이언트가 잘못된 데이터에 액세스해야 오류가 발생했습니다. 추가 유효성 검사를 수행하면 대량 로드 이후 데이터를 쿼리할 때 발생할 수 있는 예상치 못한 문제가 최소화됩니다.  
  
## <a name="bulk-exporting-or-importing-sqlxml-documents"></a>SQLXML 문서 대량 내보내기 또는 가져오기  
 SQLXML 데이터를 대량으로 내보내거나 가져오려면 서식 파일에서 다음 데이터 형식 중 하나를 사용합니다.  
  
|데이터 형식|영향|  
|---------------|------------|  
|SQLCHAR 또는 SQLVARYCHAR|데이터를 클라이언트 코드 페이지나 데이터 정렬에 포함된 코드 페이지로 보냅니다. 이는 서식 파일을 지정하지 않고 **-c** 스위치를 지정하는 것과 효과가 동일합니다.|  
|SQLNCHAR 또는 SQLNVARCHAR|데이터를 유니코드로 보냅니다. 이는 서식 파일을 지정하지 않고 **-w** 스위치를 지정하는 것과 효과가 동일합니다.|  
|SQLBINARY 또는 SQLVARYBIN|데이터를 변환하지 않고 보냅니다.|  
  
## <a name="permissions"></a>Permissions  
 **bcp out** 작업을 수행하려면 원본 테이블에 대한 SELECT 권한이 있어야 합니다.  
  
 **bcp in** 작업을 수행하려면 적어도 대상 테이블에 대한 SELECT/INSERT 권한이 있어야 합니다. 또한 다음과 같은 경우 ALTER TABLE 권한이 있어야 합니다.  
  
-   제약 조건이 있으며 CHECK_CONSTRAINTS 힌트가 지정되지 않았습니다.  
  
    > [!NOTE]
    > 기본적으로 제약 조건은 사용되지 않습니다. 제약 조건을 명시적으로 사용하려면 CHECK_CONSTRAINTS 힌트와 함께 **-h** 옵션을 사용합니다.
  
-   트리거가 있으며 FIRE_TRIGGER 힌트가 지정되지 않았습니다.  
  
    > [!NOTE]
    > 기본적으로 트리거는 실행되지 않습니다. 트리거를 명시적으로 실행하려면 FIRE_TRIGGERS 힌트와 함께 **-h** 옵션을 사용합니다.
  
-   **-E** 옵션을 사용하여 데이터 파일에서 ID 값을 가져옵니다.  
  
> [!NOTE]
> 대상 테이블에 대해 ALTER TABLE 권한이 필요하게 된 것은 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]부터였습니다. 이 요구 사항으로 인해 사용자 계정에 대상 테이블에 대한 ALTER 테이블 권한이 없을 경우 트리거 및 제약 조건 검사를 실행하지 않는 **bcp** 스크립트가 실패할 수 있습니다.
  
## <a name="character-mode--c-and-native-mode--n-best-practices"></a>문자 모드(-c) 및 기본 모드(-n) 최선의 구현 방법  
 이 섹션에는 문자 모드(-c) 및 기본 모드(-n) 사용 시의 권장 사항이 나와 있습니다.  
  
-   (관리자/사용자) 가능하면 구분 기호 문제를 방지하기 위해 기본 모드(-n)를 사용하십시오. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 사용하여 내보내기 및 가져오기를 수행하려면 기본 형식을 사용합니다. 데이터를 비 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스로 가져오려는 경우에는 -c 또는 -w 옵션을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 데이터를 내보냅니다.  
  
-   (관리자) BCP OUT를 사용할 때는 데이터를 확인합니다. 예를 들어 BCP OUT, BCP IN, BCP OUT을 차례로 사용하는 경우에는 데이터가 정상적으로 내보내기되었으며 몇몇 데이터 값의 일부분으로 종결자 값이 사용되지 않았는지 확인해야 합니다. 종결자 값과 데이터 값 간의 충돌을 방지하려면 임의의 16진수 값을 사용하여 기본 종결자를 무시할 수 있습니다(-t 및 -r 옵션 사용).  
  
-   (사용자) 실제 문자열 값 간의 충돌 가능성을 최소화하려면 길고 고유한 종결자(바이트 또는 문자 시퀀스)를 사용합니다. 이렇게 하려면 -t 및 -r 옵션을 사용하면 됩니다.  
  
## <a name="examples"></a>예  
 이 섹션에서는 다음과 같은 예를 보여 줍니다.  
 
-   1. **bcp** 유틸리티 버전 식별
  
-   2. 데이터 파일로 테이블 행 복사(트러스트된 연결 사용)  
  
-   [C.](#c-copying-table-rows-into-a-data-file-with-mixed-mode-authentication) 데이터 파일로 테이블 행 복사(혼합 모드 인증 사용)  
  
-   4. 파일에서 테이블로 데이터 복사  
  
-   5. 데이터 파일로 특정 열 복사  
  
-   6. 데이터 파일로 특정 행 복사  
  
-   7. 쿼리에서 데이터 파일로 데이터 복사  
  
-   8. 서식 파일 만들기
    
-   9. **bcp**에서 서식 파일을 사용하여 대량 가져오기 수행  


### <a name="example-test-conditions"></a>**예제 테스트 조건**
아래 예에서는 SQL Server(2016 시작) 및 Azure SQL Database에 대한 `WideWorldImporters` 샘플 데이터베이스를 사용합니다.  `WideWorldImporters`[https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0)에서 다운로드할 수 있습니다.  샘플 데이터베이스를 복원하는 구문은 [RESTORE (Transact-SQL)](../t-sql/statements/restore-statements-transact-sql.md) 을 참조하세요.  다르게 지정되지 않는 한 이 예에서는 Windows 인증을 사용하고 있고 **bcp** 명령을 실행 중인 서버 인스턴스에 트러스트된 연결이 설정되어 있다고 가정합니다.  이름이 `D:\BCP` 인 디렉터리는 많은 예제에서 사용됩니다.

다음 스크립트에서는 `WorlWideImporters.Warehouse.StockItemTransactions` 테이블의 빈 복사본을 만들고 기본 키 제약 조건을 추가합니다.  SSMS(SQL Server Management Studio)에서 다음 T-SQL 스크립트를 실행합니다.

```tsql  
USE WorlWideImporters;  
GO  

SET NOCOUNT ON;

IF NOT EXISTS (SELECT * FROM sys.tables WHERE name = 'Warehouse.StockItemTransactions_bcp')     
BEGIN
    SELECT * INTO WorlWideImporters.Warehouse.StockItemTransactions_bcp
    FROM WorlWideImporters.Warehouse.StockItemTransactions  
    WHERE 1 = 2;  

    ALTER TABLE Warehouse.StockItemTransactions_bcp 
    ADD CONSTRAINT PK_Warehouse_StockItemTransactions_bcp PRIMARY KEY NONCLUSTERED 
    (StockItemTransactionID ASC);
END
```

> [!NOTE]
> 필요에 따라 `StockItemTransactions_bcp` 테이블을 자릅니다.
>
> TRUNCATE TABLE WorlWideImporters.Warehouse.StockItemTransactions_bcp;

### <a name="a--identify-bcp-utility-version"></a>1.  **bcp** 유틸리티 버전 식별
명령 프롬프트에서 다음 명령을 입력합니다.
```
bcp -v
```
  
### <a name="b-copying-table-rows-into-a-data-file-with-a-trusted-connection"></a>2. 데이터 파일로 테이블 행 복사(트러스트된 연결 사용)  
다음 예에서는 **테이블의** out `WorlWideImporters.Warehouse.StockItemTransactions` 옵션에 대해 설명합니다.

- **Basic**  
이 예에서는 `StockItemTransactions_character.bcp` 라는 데이터 파일을 만들고 **문자** 형식을 사용하여 테이블 데이터를 파일에 복사합니다.

  명령 프롬프트에서 다음 명령을 입력합니다.
  ```
  bcp WorlWideImporters.Warehouse.StockItemTransactions out D:\BCP\StockItemTransactions_character.bcp -c -T
  ```
 
 - **Expanded**  
이 예에서는 `StockItemTransactions_native.bcp` 라는 데이터 파일을 만들고 **네이티브** 형식을 사용하여 테이블 데이터를 파일에 복사합니다.  예제에서는 또한 최대 구문 오류 수, 오류 파일 및 출력 파일을 지정합니다.

    명령 프롬프트에서 다음 명령을 입력합니다.
    ```
    bcp WorlWideImporters.Warehouse.StockItemTransactions OUT D:\BCP\StockItemTransactions_native.bcp -m 1 -n -e D:\BCP\Error_out.log -o D:\BCP\Output_out.log -S -T
    ``` 
 
`Error_out.log` 및 `Output_out.log`을 검토합니다.  `Error_out.log` 비어 있어야 합니다.  `StockItemTransactions_character.bcp` 및 `StockItemTransactions_native.bcp`간 파일 크기를 비교합니다. 
   
### <a name="c-copying-table-rows-into-a-data-file-with-mixed-mode-authentication"></a>3. 데이터 파일로 테이블 행 복사(혼합 모드 인증 사용)  
다음 예에서는 **테이블의** out `WorlWideImporters.Warehouse.StockItemTransactions` 옵션에 대해 설명합니다.  이 예에서는 `StockItemTransactions_character.bcp` 라는 데이터 파일을 만들고 **문자** 형식을 사용하여 테이블 데이터를 파일에 복사합니다.  
  
 이 예에서는 혼합 모드 인증을 사용하고 있다고 가정합니다. **-U** 스위치를 사용하여 로그인 ID를 지정해야 합니다. 또한 로컬 컴퓨터에 있는 기본 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결하지 않는 한 **-S** 스위치를 사용하여 시스템 이름을 지정하고 원하는 경우 인스턴스 이름을 지정합니다.  

명령 프롬프트에서 다음 명령을 입력합니다. \(시스템에서 암호를 입력하라는 메시지가 나타납니다.\)
```  
bcp WorlWideImporters.Warehouse.StockItemTransactions out D:\BCP\StockItemTransactions_character.bcp -c -U<login_id> -S<server_name\instance_name>
```  
  
### <a name="d-copying-data-from-a-file-to-a-table"></a>4. 파일에서 테이블로 데이터 복사  
다음 예제는 위에서 만든 파일을 사용하여 **테이블의** in `WorlWideImporters.Warehouse.StockItemTransactions_bcp` 옵션에 대해 설명합니다.
  
- **Basic**  
이 예에서는 이전에 만든 `StockItemTransactions_character.bcp` 데이터 파일을 사용합니다.

  명령 프롬프트에서 다음 명령을 입력합니다.
  ```  
  bcp WorlWideImporters.Warehouse.StockItemTransactions_bcp IN D:\BCP\StockItemTransactions_character.bcp -c -T  
  ```  

- **Expanded**  
이 예에서는 이전에 만든 `StockItemTransactions_native.bcp` 데이터 파일을 사용합니다.  예제에서는 또한 **TABLOCK**힌트를 사용하여 배치 크기, 최대 구문 오류 수, 오류 파일 및 출력 파일을 지정합니다.
  
  명령 프롬프트에서 다음 명령을 입력합니다.
  ```  
  bcp WorlWideImporters.Warehouse.StockItemTransactions_bcp IN D:\BCP\StockItemTransactions_native.bcp -b 5000 -h "TABLOCK" -m 1 -n -e D:\BCP\Error_in.log -o D:\BCP\Output_in.log -S -T 
  ```    
  `Error_in.log` 및 `Output_in.log`을 검토합니다.
   
### <a name="e-copying-a-specific-column-into-a-data-file"></a>5. 데이터 파일로 특정 열 복사  
특정 열을 복사하려면 **queryout** 옵션을 사용합니다.  다음 예에서는 `StockItemTransactionID` 테이블의 `Warehouse.StockItemTransactions` 열만 데이터 파일로 복사합니다. 
  
명령 프롬프트에서 다음 명령을 입력합니다.
  
```  
bcp "SELECT StockItemTransactionID FROM WorlWideImporters.Warehouse.StockItemTransactions WITH (NOLOCK)" queryout D:\BCP\StockItemTransactionID_c.bcp -c -T
```  
  
### <a name="f-copying-a-specific-row-into-a-data-file"></a>6. 데이터 파일로 특정 행 복사  
특정 행을 복사하려면 **queryout** 옵션을 사용합니다. 다음 예에서는 `Amy Trefl` 테이블에서 `WorlWideImporters.Application.People` 라는 연락처 행만 데이터 파일( `Amy_Trefl_c.bcp`)로 복사합니다.  참고: **-d** 스위치는 데이터베이스를 식별하는 데 사용됩니다.
  
명령 프롬프트에서 다음 명령을 입력합니다. 
```  
bcp "SELECT * from Application.People WHERE FullName = 'Amy Trefl'" queryout D:\BCP\Amy_Trefl_c.bcp -d WorlWideImporters -c -T
```  
  
### <a name="g-copying-data-from-a-query-to-a-data-file"></a>7. 쿼리에서 데이터 파일로 데이터 복사  
Transact-SQL 문의 결과 집합을 데이터 파일로 복사하려면 **queryout** 옵션을 사용합니다.  다음 예에서는 `WorlWideImporters.Application.People` 테이블에서 전체 이름을 기준으로 정렬된 이름을 `People.txt` 데이터 파일로 복사합니다.  참고: **-t** 스위치는 쉼표로 구분된 파일을 만드는 데 사용됩니다.
  
명령 프롬프트에서 다음 명령을 입력합니다.
```  
bcp "SELECT FullName, PreferredName FROM WorlWideImporters.Application.People ORDER BY FullName" queryout D:\BCP\People.txt -t, -c -T
```  
  
### <a name="h-creating-format-files"></a>8. 서식 파일 만들기  
다음 예에서는 `Warehouse.StockItemTransactions` 데이터베이스의 `WorlWideImporters` 테이블에 대해 3개의 서로 다른 서식 파일을 만듭니다.  만들어진 각 파일의 내용을 검토합니다.
  
명령 프롬프트에서 다음 명령을 입력합니다.
  
```  
REM non-XML character format
bcp WorlWideImporters.Warehouse.StockItemTransactions format nul -f D:\BCP\StockItemTransactions_c.fmt -c -T 

REM non-XML native format
bcp WorlWideImporters.Warehouse.StockItemTransactions format nul -f D:\BCP\StockItemTransactions_n.fmt -n -T

REM XML character format
bcp WorlWideImporters.Warehouse.StockItemTransactions format nul -f D:\BCP\StockItemTransactions_c.xml -x -c -T
 
```  
  
> [!NOTE]  
>  **-x** 스위치를 사용하려면 **bcp** 9.0 클라이언트를 사용해야 합니다. **bcp** 9.0 클라이언트를 사용하는 방법은 "[주의](#remarks)"를 참조하세요.  
  
 자세한 내용은 [비 XML 서식 파일&#40;SQL Server&#41;](../relational-databases/import-export/non-xml-format-files-sql-server.md) 및 [XML 서식 파일&#40;SQL Server&#41;](../relational-databases/import-export/xml-format-files-sql-server.md)을 참조하세요.  
  
### <a name="i-using-a-format-file-to-bulk-import-with-bcp"></a>9. bcp에서 서식 파일을 사용하여 대량 가져오기 수행  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스로 데이터를 가져올 때 이전에 만든 서식 파일을 사용하려면 **in** 옵션과 함께 **-f** 스위치를 사용합니다.  예를 들어 다음 명령은 이전에 만든 서식 파일인 `StockItemTransactions_character.bcp`을 사용하여 데이터 파일 `Warehouse.StockItemTransactions_bcp` 의 내용을 `StockItemTransactions_c.xml`테이블의 복사본으로 대량 복사합니다.  참고: **-L** 스위치는 처음 100개의 레코드를 가져오는 데 사용됩니다.
  
명령 프롬프트에서 다음 명령을 입력합니다.
```  
bcp WorlWideImporters.Warehouse.StockItemTransactions_bcp in D:\BCP\StockItemTransactions_character.bcp -L 100 -f D:\BCP\StockItemTransactions_c.xml -T 
```  
  
> [!NOTE]  
>  데이터 파일 필드와 테이블 열의 숫자, 순서, 데이터 형식 등이 다른 경우 서식 파일을 사용하면 유용합니다. 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)에 대한 지식이 필요하지 않습니다.  
  
### <a name="j-specifying-a-code-page"></a>10. 코드 페이지 지정  
 다음 부분 코드 예제에서는 코드 페이지 65001을 지정하는 동안 bcp 가져오기를 보여 줍니다.  
  
```  
bcp.exe MyTable in "D:\data.csv" -T -c -C 65001 -t , ...  
```  
  
 다음 부분 코드 예제에서는 코드 페이지 65001을 지정하는 동안 bcp 내보내기를 보여 줍니다.  
  
```  
bcp.exe MyTable out "D:\data.csv" -T -c -C 65001 -t , ...  
```  
  
## <a name="additional-examples"></a>추가 예  
|다음 항목에는 bcp를 사용하는 예제가 포함되어 있습니다. |
|---|
|대량 가져오기 또는 대량 내보내기를 위한 데이터 형식(SQL Server)<br />&emsp;&#9679;&emsp;[네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기(SQL Server)](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[문자 형식을 사용하여 데이터 가져오기 또는 내보내기(SQL Server)](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[데이터를 가져오거나 내보내기 위해 유니코드 네이티브 형식 사용(SQL Server)](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[유니코드 문자 형식을 사용하여 데이터 가져오기 및 내보내기(SQL Server)](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)<br /><br />[필드 및 행 종결자 지정(SQL Server)](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)<br /><br />[대량 가져오기 수행 중 Null 유지 또는 기본값 사용(SQL Server)](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)<br /><br />[데이터 대량 가져오기 중 ID 값 유지(SQL Server)](../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)<br /><br />데이터를 가져오거나 내보내기 위한 서식 파일(SQL Server)<br />&emsp;&#9679;&emsp;[서식 파일 만들기(SQL Server)](../relational-databases/import-export/create-a-format-file-sql-server.md)<br />&emsp;&#9679;&emsp;[서식 파일을 사용하여 데이터 대량 가져오기(SQL Server)](../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)<br />&emsp;&#9679;&emsp;[서식 파일을 사용하여 테이블 열 건너뛰기(SQL Server)](../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)<br />&emsp;&#9679;&emsp;[서식 파일을 사용하여 데이터 필드 건너뛰기(SQL Server)](../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)<br />&emsp;&#9679;&emsp;[서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑(SQL Server)](../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)<br /><br />[XML 문서 대량 가져오기 및 내보내기 예(SQL Server)](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)<br /><p>                                                                                                                                                                                                                  </p>|

## <a name="see-also"></a>관련 항목:  
 [대량 내보내기 또는 가져오기 &#40;에 대 한 데이터를 준비 합니다. SQL Server &#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../t-sql/functions/openrowset-transact-sql.md)   
 [SET quoted_identifier&#40; Transact SQL &#41;](../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [sp_configure&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_tableoption &#40; Transact SQL &#41;](../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)   
 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)  
  
  
