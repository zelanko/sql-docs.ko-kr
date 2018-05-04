---
title: Bcp를 사용 하 여 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- bcp
ms.assetid: 3eca5717-e50f-40db-be16-a1cebbdfee70
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58e5a45775a52113d93b2fad93797274adb71b78
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-with-bcp"></a>bcp를 사용하여 연결
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[bcp](http://go.microsoft.com/fwlink/?LinkID=190626) 유틸리티는에서 사용할 수는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Linux와 macOS에서 합니다. 이 페이지의 Windows 버전 간의 차이점을 문서화 `bcp`합니다.
  
- 필드 종결자는 탭("\t")입니다.  
  
- 줄 종결자는 줄 바꿈 문자("\n")입니다.  
  
- 문자 모드는 기본 설정된 된 형식에 대 한 `bcp` 파일과 확장된 문자를 포함 하지 않는 데이터 파일 형식을 지정 합니다.  
  
> [!NOTE]  
> 백슬래시 '\\'에 명령줄 인수 quoted 이거나 이스케이프 합니다. 예를 들어 사용자 지정 행 종결자로 줄 바꿈 문자를 지정 하려면 다음 메커니즘 중 하나 사용 해야 하면:  
>   
> -   -r\\\n  
> -   -r"\n"  
> -   -r'\n'  
  
다음은의 샘플 명령 호출 `bcp` 를 텍스트 파일로 테이블 행을 복사 하려면:  
  
```  
bcp AdventureWorks2008R2.Person.Address out test.dat -Usa -Pxxxx -Sxxx.xxx.xxx.xxx  
```  
  
## <a name="available-options"></a>사용 가능한 옵션
현재 릴리스에서 다음 구문 및 옵션 사용할 수 있습니다.  

[*데이터베이스 ***.**]* 스키마 ***.*** 테이블 * **에** *data_file* | **아웃** *data_file*

- -a *packet_size*  
서버에서 전송되거나 서버로 전송되는 네트워크 패킷당 바이트 수를 지정합니다.  
  
- -b *batch_size*  
가져온 데이터의 일괄 처리당 행 수를 지정합니다.  
  
- -c  
문자 데이터 형식 사용  
  
- -d *database_name*  
연결할 데이터베이스를 지정합니다.  
  
- -d  
에 전달 된 값이 고 `bcp` -S 옵션이 데이터 원본 이름 (DSN)으로 해석 되도록 합니다. 자세한 내용은에서 "sqlcmd 및 bcp에서 DSN 지원" 참조 [sqlcmd를 사용 하 여 연결](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)합니다.  
  
- -e *error_file* 행을 저장 하는 데 사용 되는 오류 파일의 전체 경로 지정 된 `bcp` 유틸리티는 파일에서 데이터베이스로 전송할 수 없습니다.  
  
- -e  
가져온 데이터 파일의 ID 값을 ID 열에 사용합니다.  
  
- -f *format_file*  
서식 파일의 전체 경로를 지정합니다.  
  
- -F *first_row*  
테이블에서 내보내거나 데이터 파일에서 가져올 첫 번째 행 번호를 지정합니다.  
  
- -k  
작업 시 삽입된 열에 기본값이 지정되지 않고 빈 열이 Null 값을 보유하도록 지정합니다.  
  
- -l  
로그인 시간 제한을 지정합니다. 에 대 한 로그인 시간 (초)의 수를 지정 하는 – l 옵션 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 시간 초과 서버에 연결 하려고 합니다. 기본 로그인 제한 시간은 15 초입니다. 로그인 제한 시간을 0에서 65534 사이의 숫자 여야 합니다. 입력한 값이 숫자가 아니거나 이 범위에 속하지 않을 경우 `bcp`는 오류 메시지를 생성합니다. 값이 0에는 무한 시간 제한을 지정합니다.
  
- -L *last_row*  
테이블에서 내보내거나 데이터 파일에서 가져올 마지막 행 번호를 지정합니다.  
  
- -m *max_errors*  
구문 오류가 발생할 수 있는 최대 수를 지정 된 `bcp` 작업을 취소 합니다.  
  
- -n  
데이터의 네이티브(데이터베이스) 데이터 형식을 사용하여 대량 복사 작업을 수행합니다.  
  
- -P *password*  
로그인 ID의 암호를 지정합니다.  
  
- -Q  
`bcp` 유틸리티와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 인스턴스 간의 연결에서 SET QUOTED_IDENTIFIERS ON 문을 실행합니다.  
  
- -r *row_terminator*  
행 종결자를 지정합니다.  
  
- -r  
클라이언트 컴퓨터의 로캘 설정에 정의된 국가별 형식을 사용하여 통화, 날짜 및 시간 데이터를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]로 대량 복사하도록 지정합니다.  
  
- -S *server*  
이름을 지정는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 에 연결 하는 인스턴스 또는-D는 경우를 사용 하는 DSN입니다.  
  
- -t *field_terminator*  
필드 종결자를 지정합니다.  
  
- -T  
지정 된 `bcp` 유틸리티에 연결 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 트러스트 된 연결 사용 (통합된 보안).  
  
- -U *login_id*  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 연결에 사용하는 로그인 ID를 지정합니다.  
  
- -v  
`bcp` 유틸리티 버전 번호 및 저작권을 보고합니다.  
  
- -w  
유니코드 문자를 사용하여 대량 복사 작업을 수행합니다.  
  
이 릴리스에서는 Latin-1과 UTF-16 문자가 지원됩니다.  
  
## <a name="unavailable-options"></a>사용할 수 없는 옵션
현재 릴리스에서 다음 구문 및 옵션 사용할 수 없습니다.  

- -c  
데이터 파일에서 데이터의 코드 페이지를 지정합니다.  
  
- -h *hint*  
데이터를 테이블 또는 뷰로 대량으로 가져오는 동안 사용되는 힌트를 지정합니다.  
  
- -i *input_file*  
지시 파일의 이름을 지정합니다.  
  
- -n  
문자가 아닌 데이터의 경우 데이터의 네이티브(데이터베이스) 데이터 형식을 사용하고 문자 데이터의 경우 유니코드 문자를 사용합니다.  
  
- -o *output_file*  
명령 프롬프트에서 리디렉션된 출력을 받는 파일의 이름을 지정합니다.  
  
- -V (80 | 90 | 100)  
이전 버전의 데이터 형식을 사용 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다.  
  
- -X  
서식 및 -f format_file 옵션과 함께 사용되며 기본 비 XML 서식 파일 대신 XML 기반 서식 파일을 생성합니다.  
  
## <a name="see-also"></a>관련 항목:

[사용 하 여 연결 **sqlcmd**](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)  
