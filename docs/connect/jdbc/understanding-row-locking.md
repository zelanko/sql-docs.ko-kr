---
title: 행 잠금 이해 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 63c76a2f-f2b9-461f-8904-acbda0169ac3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bcd18baf401378605abf0d53e203d0a3745ee887
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027331"
---
# <a name="understanding-row-locking"></a>행 잠금 이해

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 행 잠금을 사용합니다. 행 잠금은 데이터베이스에서 동시에 수정 작업을 수행하는 여러 사용자 사이의 동시성 제어를 구현합니다. 기본적으로 트랜잭션 및 잠금은 각 연결마다 관리됩니다. 예를 들어 애플리케이션이 두 개의 JDBC 연결을 열 경우 한 연결에서 설정한 잠금은 다른 연결에서 공유할 수 없습니다. 연결은 다른 연결에서 보유한 잠금과 충돌하는 잠금을 설정할 수 없습니다.

> [!NOTE]  
> 행 잠금이 사용되면 인출 버퍼의 모든 행에 잠금이 수행되므로 인출 크기에 매우 큰 값을 설정하면 동시성에 영향을 줄 수 있습니다.

잠금은 트랜잭션 무결성 및 데이터베이스 동시성을 보장하는 데 사용됩니다. 잠금은 다른 사용자가 변경하고 있는 데이터를 렌더링할 수 없도록 하고 여러 사용자가 동일한 데이터를 동시에 변경하지 못하도록 합니다. 잠금 기능을 사용하지 않으면 데이터베이스 내의 데이터가 논리적으로 올바르지 않게 되고, 해당 데이터에 대해 실행한 쿼리에서 예상치 못한 결과가 발생할 수 있습니다.

> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 행 잠금에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "[!INCLUDE[ssDE](../../includes/ssde_md.md)]에서의 잠금"을 참조하세요.

## <a name="see-also"></a>참고 항목

[JDBC 드라이버로 결과 집합 관리](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)
