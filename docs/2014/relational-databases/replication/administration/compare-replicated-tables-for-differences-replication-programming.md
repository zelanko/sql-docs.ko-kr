---
title: 복제된 테이블의 차이점 비교(복제 프로그래밍) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- tablediff utility
- comparing replicated tables
ms.assetid: cd253a17-0c85-42b4-912c-690169ebe799
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4a7d6315a8d8237effe5ae888d303e3aab0dcef1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85038410"
---
# <a name="compare-replicated-tables-for-differences-replication-programming"></a>복제된 테이블의 차이점 비교(복제 프로그래밍)
  아티클 유효성 검사는 게시자 및 구독자에서 테이블 아티클의 게시된 데이터가 일치하지 않는지 여부를 확인하는 데 사용됩니다. 자세한 내용은 [복제된 데이터의 유효성 검사](../validate-data-at-the-subscriber.md)를 참조하세요. 그러나 유효성 검사를 통해서는 성공 또는 실패 정보만 반환되고 원본 테이블과 대상 테이블의 차이점에 대한 정보는 제공되지 않습니다. **tablediff** 명령 프롬프트 유틸리티는 두 테이블 간의 세부 차이점 정보를 반환하며 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트를 생성하여 구독이 게시자의 데이터와 일치하게 할 수도 있습니다.  
  
> [!NOTE]  
>  **tablediff** 유틸리티는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서버에서만 지원됩니다.  
  
### <a name="to-compare-replicated-tables-for-differences-using-tablediff"></a>tablediff를 사용하여 복제된 테이블의 차이점을 비교하려면  
  
1.  복제 토폴로지에 있는 서버의 명령 프롬프트에서 [tablediff Utility](../../../tools/tablediff-utility.md)를 실행합니다. 다음 매개 변수를 지정합니다.  
  
    -   **-sourceserver** - 올바른 데이터가 있는 서버(대개 게시자)의 이름입니다.  
  
    -   **-sourcedatabase** - 올바른 데이터가 들어 있는 데이터베이스의 이름입니다.  
  
    -   **-sourcetable** - 비교할 아티클의 원본 테이블 이름입니다.  
  
    -   **-sourceschema** (옵션) - 원본 테이블의 스키마 소유자입니다(기본 스키마가 아닌 경우).  
  
    -   **-sourceuser** 및 **-sourcepassword** (옵션) - SQL Server 인증을 사용하여 게시자에 연결할 경우에 지정합니다.  
  
        > [!IMPORTANT]  
        >  가능하면 Windows 인증을 사용하세요. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용해야 하는 경우에는 런타임에 사용자에게 보안 자격 증명을 지정하라는 메시지가 표시되도록 하십시오. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
    -   **-destinationserver** - 데이터를 비교할 서버(대개 구독자)의 이름입니다.  
  
    -   **-destinationdatabase** - 비교할 데이터베이스의 이름입니다.  
  
    -   **-destinationtable** - 비교할 테이블의 이름입니다.  
  
    -   **-destinationschema** (옵션) - 대상 테이블의 스키마 소유자입니다(기본 스키마가 아닌 경우).  
  
    -   **-destinationuser** 및 **-destinationpassword** (옵션) - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하여 구독자에 연결할 경우에 지정합니다.  
  
        > [!IMPORTANT]  
        >  가능하면 Windows 인증을 사용하세요. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용해야 하는 경우에는 런타임에 사용자에게 보안 자격 증명을 지정하라는 메시지가 표시되도록 하십시오. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
    -   **-c** (옵션) - 열 수준 비교를 수행하려는 경우에 사용합니다.  
  
    -   **-q** (옵션) - 행 개수 전용 및 스키마 전용 비교를 수행하려는 경우에 사용합니다.  
  
    -   **-o** (옵션) - 결과를 파일로 출력하려면 이 매개 변수에 파일 이름 및 경로를 지정합니다.  
  
    -   **-et**(옵션) - 결과를 삽입할 구독 데이터베이스의 테이블을 지정합니다. 해당 테이블이 이미 있는 경우 **-dt** 를 지정하여 먼저 해당 테이블을 삭제합니다.  
  
    -   **-f** (옵션) - 구독자의 데이터를 게시자의 데이터와 일치하게 수정하려면 이 매개 변수를 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 파일을 생성합니다. 각 파일의 **문 수를 지정하려면** -df [!INCLUDE[tsql](../../../includes/tsql-md.md)] 를 사용합니다.  
  
    -   **-rc** 및 **-ri** (옵션) - 작업을 다시 시도할 횟수와 다시 시도 간격을 지정하려는 경우에 사용합니다.  
  
    -   **-strict** (옵션) - 원본 테이블과 대상 테이블 간의 엄격한 스키마 비교를 적용하려는 경우에 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [구독자에서 데이터 유효성 검사](../validate-data-at-the-subscriber.md)  
  
  
