---
title: 클라이언트 프로토콜 속성(순서 탭)
description: 클라이언트 프로토콜을 사용하거나 사용하지 않도록 설정하는 방법을 알아봅니다. 클라이언트가 SQL Server에 연결하려고 할 때 프로토콜을 사용하는 순서를 다시 정렬하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- client protocols [SQL Server]
ms.assetid: 64fd7135-1756-4885-bed9-9ab8997ecc6c
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: b4b16ac626cc68b6b989aa9c68d9ce93b69b6820
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88900561"
---
# <a name="client-protocols-properties-order-tab"></a>클라이언트 프로토콜 속성(순서 탭)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  **클라이언트 프로토콜 속성** 대화 상자의 **순서**페이지를 사용하여 클라이언트 프로토콜을 확인하고 설정할 수 있습니다.  
  
 선택한 프로토콜을 **사용할 수 없는 프로토콜** 또는 **사용할 수 있는 프로토콜** 목록으로 이동하려면 해당 프로토콜을 클릭한 다음 **사용** 또는 **사용 안 함** 을 클릭합니다.  
  
 목록의 맨 위에 있는 프로토콜에 먼저 연결을 시도한 다음 두 번째 프로토콜에 연결하는 식으로 목록에 나오는 순서대로 연결 시도가 진행됩니다. 위쪽 화살표 단추나 아래쪽 화살표 단추를 클릭하여 **사용할 수 있는 프로토콜** 목록의 위나 아래로 프로토콜을 이동할 수 있습니다. 서버와 동일한 컴퓨터에서 실행되는 클라이언트가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 때는 **공유 메모리** 프로토콜을 맨 먼저 사용합니다(사용하는 경우).  
  
> [!NOTE]  
>  이러한 설정은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET SqlClient에서는 사용되지 않습니다. .NET SqlClient에 대한 프로토콜 순서는 첫 번째가 TCP이고 그 다음이 명명된 파이프이며 이 순서는 변경할 수 없습니다.  
  
## <a name="options"></a>옵션  
 **사용**  
 설치되어 있지만 현재 사용되지 않는 프로토콜을 나열합니다.  
  
 **사용 안 함**  
 이 컴퓨터의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트에 사용할 수 있는 프로토콜을 나열합니다.  
  
 **>**  
 **사용할 수 없는 프로토콜** 상자에서 선택한 프로토콜을 **사용할 수 있는 프로토콜** 상자로 이동하여 사용할 수 있도록 만듭니다.  
  
 **\<**  
 **사용할 수 있는 프로토콜** 상자에서 선택한 프로토콜을 **사용할 수 없는 프로토콜** 상자로 이동하여 사용할 수 없도록 만듭니다.  
  
 위쪽 화살표  
 목록에서 선택한 프로토콜을 위로 이동합니다. 이렇게 하면 연결할 때 Net-Library에서 해당 프로토콜을 먼저 사용하도록 프로토콜의 우선 순위를 높일 수 있습니다.  
  
 아래쪽 화살표  
 목록에서 선택한 프로토콜을 아래로 이동합니다. 이렇게 하면 연결할 때 Net-Library에서 해당 프로토콜을 나중에 사용하도록 프로토콜의 우선 순위를 낮출 수 있습니다.  
  
 **공유 메모리 프로토콜 사용**  
 서버와 동일한 컴퓨터에서 실행되는 클라이언트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결할 때 항상 맨 먼저 연결을 시도하는 공유 메모리 프로토콜을 설정합니다(사용하는 경우).  
  
> [!NOTE]  
>  접두사를 통해 또는 연결 문자열의 일부로 프로토콜을 지정하면 지정한 프로토콜에 대해서만 연결이 시도됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [네트워크 프로토콜 선택](/previous-versions/sql/sql-server-2016/ms187892(v=sql.130))  
  
