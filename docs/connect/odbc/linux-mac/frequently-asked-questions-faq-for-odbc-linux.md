---
title: ODBC Linux 및 macOS에 대한 FAQ(질문과 대답) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d199b4cb7120be85c50eda758e27330705ff6fe9
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786744"
---
# <a name="frequently-asked-questions-faq-for-odbc-linux-and-macos"></a>ODBC Linux 및 macOS에 대한 FAQ(질문과 대답)
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

다음은 Linux 및 macOS 기반 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 관련된 질문에 대한 대답입니다.
  
## <a name="frequently-asked-questions"></a>질문과 대답

**Linux 또는 macOS 기반 기존 ODBC 응용 프로그램이 어떻게 드라이버에서 작동하나요?**  
다른 드라이버를 사용 중인 Linux 또는 macOS에서 컴파일하고 실행한 ODBC 응용 프로그램을 컴파일하고 실행할 수 있어야 합니다. 
  
**[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]의 어떤 기능이 이 버전의 드라이버를 지원하나요?**

Linux 또는 macOS 기반 ODBC 드라이버는 LocalDB를 제외한 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 의 모든 서버 기능을 지원합니다. 에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 지원 되는 기능을 참조 하세요 [Programming Guidelines](../../../connect/odbc/linux-mac/programming-guidelines.md)합니다.  
  
**드라이버가 Kerberos 인증을 지원하나요?**  
예 사용 하 여 서버에 연결할 수 있어야는 기존 Kerberos 환경 설정에 있는 경우는 `Trusted_Connection=Yes` DSN 또는 연결 문자열 옵션입니다. 자세한 내용은 [Using Integrated Authentication](../../../connect/odbc/linux-mac/using-integrated-authentication.md)을 참조하세요.  
  
**응용 프로그램이 어떤 유니코드 인코딩을 사용해야 하나요?**  
SQL_CHAR 데이터는 UTF-8을 사용하고 SQL_WCHAR 데이터는 UTF-16을 사용합니다.  

**실험하거나 평가하기 위해 드라이버를 사용하여 실행할 수 있는 ODBC 샘플을 다운로드할 수 있나요?**

샘플은 [Linux 기반 ODBC 드라이버에 대해 기존 MSDN C++ ODBC 샘플 사용](http://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) 을 참조하세요. MacOS의 ODBC 드라이버에 적용할 수 이기도합니다. 

**Linux 기반 ODBC 드라이버는 macOS 오픈 소스 여부**

아니요, Linux 및 macOS에서 ODBC 드라이버는 오픈 소스 제품 않습니다.  

## <a name="see-also"></a>참고 항목
[Linux 및 macOS 기반 SQL Server용 Microsoft ODBC Driver 설치](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
