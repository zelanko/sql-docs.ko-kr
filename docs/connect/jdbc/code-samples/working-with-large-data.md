---
title: 큰 데이터 작업 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5b93569f-eceb-4f05-b49c-067564cd3c85
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 425beac7bcae36170ff378b59d36da05838df645
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69028249"
---
# <a name="working-with-large-data"></a>대규모 데이터 작업

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

JDBC 드라이버에서는 서버 커서 오버헤드 없이 모든 종류의 큰 값 데이터를 검색할 수 있는 선택 버퍼링이 지원됩니다. 적응 버퍼링을 사용하면 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 문 실행 결과를 한 번에 모두 검색하는 것이 아니라 애플리케이션에 필요할 때 검색합니다. 또한 애플리케이션에서 더 이상 액세스할 수 없는 결과를 즉시 삭제합니다.  
  
[!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] JDBC 드라이버 버전 1.2에서 버퍼링 모드의 기본값은 "**full**"이었습니다. 즉 애플리케이션에서 연결 속성 또는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체의 [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 메서드를 사용하여 "responseBuffering" 연결 속성을 "**adaptive**"로 설정하지 않은 경우 이 드라이버에서는 전체 결과를 서버에서 한 번에 읽어오는 동작이 지원됩니다. 적응 버퍼링 동작을 사용하려면 애플리케이션에서 명시적으로 "responseBuffering" 연결 속성을 "**adaptive**"로 설정해야 합니다.  
  
**adaptive** 값이 기본 버퍼링 모드이며 JDBC 드라이버는 필요에 따라 가능한 최소한의 데이터를 버퍼링합니다. 적응 버퍼링 사용에 대한 자세한 내용은 [적응 버퍼링 사용](../../../connect/jdbc/using-adaptive-buffering.md)을 참조하세요.  
  
이 섹션의 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에서 큰 값 데이터를 검색하는 데 사용할 수 있는 여러 가지 방법에 대해 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
| 항목                                                                                                                         | Description                                                              |
| ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| [대규모 데이터 읽기 샘플](../../../connect/jdbc/code-samples/reading-large-data-sample.md)                                               | SQL 문을 사용하여 큰 값 데이터를 검색하는 방법에 대해 설명합니다.       |
| [저장 프로시저에서 대규모 데이터 읽기 샘플](../../../connect/jdbc/code-samples/reading-large-data-with-stored-procedures-sample.md) | 큰 CallableStatement OUT 매개 변수 값을 검색하는 방법에 대해 설명합니다. |
| [대규모 데이터 업데이트 샘플](../../../connect/jdbc/code-samples/updating-large-data-sample.md)                                             | 데이터베이스에서 큰 값 데이터를 업데이트하는 방법에 대해 설명합니다.                |
  
## <a name="see-also"></a>참고 항목

[샘플 JDBC 드라이버 애플리케이션](../../../connect/jdbc/code-samples/sample-jdbc-driver-applications.md)  
  
