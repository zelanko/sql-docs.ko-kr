---
title: "자주 질문과 대답 (FAQ)에 대해 ODBC Linux와 macOS | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aa835ce2bb9e35191d9c3056dad2f208445c361a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="frequently-asked-questions-faq-for-odbc-linux-and-macos"></a>자주 질문과 대답 (FAQ) ODBC Linux와 macOS에 대 한
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

다음은에 대 한 ODBC 드라이버에 대 한 질문에 대답 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Linux와 macOS에서 합니다.
  
## <a name="frequently-asked-questions"></a>질문과 대답

**드라이버와 함께 Linux 또는 macOS에서 기존 ODBC 응용 프로그램은 어떻게 작동 하나요?**  
컴파일하고 있습니다 컴파일하고 Linux 또는 다른 드라이버를 사용 하 여 macOS에서 실행 되는 ODBC 응용 프로그램을 실행할 수 있습니다. 
  
**어떤 기능이 [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] 버전은이 버전의 드라이버 지원?**

Linux와 macOS에서 ODBC 드라이버는의 모든 서버 기능을 지원 [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] LocalDB를 제외한 합니다. 에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 지원 되는 기능 참조 [프로그래밍 지침](../../../connect/odbc/linux-mac/programming-guidelines.md)합니다.  
  
**드라이버가는 Kerberos 인증을 지원 하나요?**  
예 사용 하 여 서버에 연결할 수 있어야 기존 Kerberos 환경 설치를 사용 하도록 설정한 경우는 `Trusted_Connection=Yes` DSN 또는 연결 문자열 옵션입니다. 자세한 내용은 참조 [통합 인증을 사용](../../../connect/odbc/linux-mac/using-integrated-authentication.md)합니다.  
  
**어떤 유니코드 인코딩을 해야 응용 프로그램 사용?**  
SQL_CHAR 데이터는 UTF-8을 사용하고 SQL_WCHAR 데이터는 UTF-16을 사용합니다.  

**다운로드 하 고 드라이버 시험해를 평가 하기를 사용 하 여 실행 하는 ODBC 예제 있나요?**

샘플은 [Linux 기반 ODBC 드라이버에 대해 기존 MSDN C++ ODBC 샘플 사용](http://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) 을 참조하세요. MacOS ODBC 드라이버에 적용할 수 이기도합니다. 

**Linux 기반 ODBC 드라이버 인가요 아니면 macOS 오픈 소스?**

아니요, Linux와 macOS에서 ODBC 드라이버는 오픈 소스 제품 않습니다.  

## <a name="see-also"></a>관련 항목:
[Microsoft ODBC Driver for Linux와 macOS에서 SQL Server 설치](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

