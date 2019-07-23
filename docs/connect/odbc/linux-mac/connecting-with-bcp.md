---
title: Bcp를 사용 하 여 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bcp
ms.assetid: 3eca5717-e50f-40db-be16-a1cebbdfee70
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1dd80df3a0f7fabec7ae9ddc51b16cb4456c7970
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996613"
---
# <a name="connecting-with-bcp"></a>bcp를 사용하여 연결
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[bcp](https://go.microsoft.com/fwlink/?LinkID=190626) 유틸리티는 Linux 및 macOS 기반 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 사용할 수 있습니다. 이 페이지에서는 Windows 버전의 `bcp`차이점을 설명 합니다.
  
- 필드 종결자는 탭("\t")입니다.  
  
- 줄 종결자는 줄 바꿈 문자("\n")입니다.  
  
- 문자 모드는 확장된 문자를 포함하지 않는 `bcp` 서식 파일 및 데이터 파일의 기본 형식입니다.  
  
> [!NOTE]  
> 명령줄 인수에서 백슬래시 '\\'는 따옴표로 묶거나 이스케이프되어야 합니다. 예를 들어 사용자 지정 행 종결자로 줄 바꿈 문자를 지정하려면 다음 메커니즘 중 하나를 사용해야 합니다.  
>   
> -   -r\\\n  
> -   -r"\n"  
> -   -r'\n'  
  
다음은 텍스트 파일로 테이블 행을 복사하는 `bcp`의 샘플 명령 호출입니다.  
  
```  
bcp AdventureWorks2008R2.Person.Address out test.dat -Usa -Pxxxx -Sxxx.xxx.xxx.xxx  
```  
  
## <a name="available-options"></a>사용 가능한 옵션
현재 릴리스에서 다음 구문 및 옵션을 사용할 수 있습니다.  

[_database_ **.** ]_schema_ **.** _table_ **in** _data\_file_ | **out** _data\_file_

- -a *packet_size*  
서버에서 전송되거나 서버로 전송되는 네트워크 패킷당 바이트 수를 지정합니다.  
  
- -b *batch_size*  
가져온 데이터의 일괄 처리당 행 수를 지정합니다.  
  
- -c  
문자 데이터 형식 사용  
  
- -d *database_name*  
연결할 데이터베이스를 지정합니다.  
  
- -d  
`bcp` -S 옵션에 전달된 값이 DSN(데이터 원본 이름)으로 해석되도록 합니다. 자세한 내용은 [Connecting with sqlcmd](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)에서 "sqlcmd 및 bcp에서 DSN 지원"을 참조하세요.  
  
- -e *error_file* `bcp` 유틸리티가 파일에서 데이터베이스로 전송할 수 없는 행을 저장하는 데 사용되는 오류 파일의 전체 경로를 지정합니다.  
  
- -E  
가져온 데이터 파일의 ID 값을 ID 열에 사용합니다.  
  
- -f *format_file*  
서식 파일의 전체 경로를 지정합니다.  
  
- -F *first_row*  
테이블에서 내보내거나 데이터 파일에서 가져올 첫 번째 행 번호를 지정합니다.  
  
- -k  
작업 시 삽입된 열에 기본값이 지정되지 않고 빈 열이 Null 값을 보유하도록 지정합니다.  
  
- -l  
로그인 시간 제한을 지정합니다. -l 옵션을 사용하여 서버에 연결을 시도할 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 로그인 제한 시간(초)을 지정합니다. 기본 로그인 제한 시간은 15 초입니다. 로그인 제한 시간은 0에서 65534 사이의 숫자여야 합니다. 입력한 값이 숫자가 아니거나 이 범위에 속하지 않을 경우 `bcp`는 오류 메시지를 생성합니다. 값 0은 무한 시간 제한을 지정 합니다.
  
- -L *last_row*  
테이블에서 내보내거나 데이터 파일에서 가져올 마지막 행 번호를 지정합니다.  
  
- -m *max_errors*  
`bcp` 작업이 취소되는 최대 구문 오류 발생 횟수를 지정합니다.  
  
- -n  
데이터의 네이티브(데이터베이스) 데이터 형식을 사용하여 대량 복사 작업을 수행합니다.  
  
- -P *password*  
로그인 ID의 암호를 지정합니다.  
  
- -Q  
`bcp` 유틸리티와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 간의 연결에서 SET QUOTED_IDENTIFIERS ON 문을 실행합니다.  
  
- -r *row_terminator*  
행 종결자를 지정합니다.  
  
- -r  
클라이언트 컴퓨터의 로캘 설정에 정의된 국가별 형식을 사용하여 통화, 날짜 및 시간 데이터를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로 대량 복사하도록 지정합니다.  
  
- -S *server*  
연결할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정 하거나,-D를 사용 하는 경우 DSN을 지정 합니다.  
  
- -t *field_terminator*  
필드 종결자를 지정합니다.  
  
- -T  
`bcp` 유틸리티가 신뢰할 수 있는 연결을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 연결되도록 지정합니다(통합 보안).  
  
- -U *login_id*  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]연결에 사용하는 로그인 ID를 지정합니다.  
  
- -V  
`bcp` 유틸리티 버전 번호 및 저작권을 보고합니다.  
  
- -w  
유니코드 문자를 사용하여 대량 복사 작업을 수행합니다.  
  
이 릴리스에서는 Latin-1과 UTF-16 문자가 지원됩니다.  
  
## <a name="unavailable-options"></a>사용할 수 없는 옵션
현재 릴리스에서는 다음 구문 및 옵션을 사용할 수 없습니다.  

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
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]이전 버전의 데이터 형식을 사용합니다.  
  
- -X  
서식 및 -f format_file 옵션과 함께 사용되며 기본 비 XML 서식 파일 대신 XML 기반 서식 파일을 생성합니다.  
  
## <a name="see-also"></a>참고 항목

[**sqlcmd**를 사용하여 연결](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)  
