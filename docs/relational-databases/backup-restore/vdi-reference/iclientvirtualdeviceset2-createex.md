---
title: IClientVirtualDeviceSet2::CreateEx
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IClientVirtualDeviceSet2::CreateEx 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 90165738dfcea8818353d602f72390bb08eea792
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847354"
---
# <a name="iclientvirtualdeviceset2createex-vdi"></a>IClientVirtualDeviceSet2::CreateEx (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**CreateEx** 함수는 가상 디바이스 세트를 만듭니다.

## <a name="syntax"></a>구문

```c
HRESULT IClientVirtualDeviceSet2::CreateEx (
   LPCWSTR         lpInstanceName,
   LPCWSTR         lpName,
   VDConfig*      pCfg
);
```

## <a name="parameters"></a>매개 변수

*lpInstanceName* 이 문자열은 SQL 명령이 전송될 SQL Server 인스턴스를 식별합니다.

*lpName* 가상 디바이스 세트를 식별합니다. CreateFileMapping()에서 사용되는 이름에 대한 규칙을 따라야 합니다. 백슬래시(\))를 제외한 모든 문자를 사용할 수 있습니다. 와이드 문자 유니코드 문자열입니다. 사용자의 제품 또는 회사 이름과 데이터베이스 이름이 포함된 문자열을 접두사로 사용하는 것이 좋습니다.

*pCfg* 가상 디바이스 세트의 구성입니다. 자세한 내용은 구성을 참조하세요.

## <a name="return-value"></a>반환 값

|반환 값 | 설명 |
|---|---|
| NOERROR | 함수가 성공했습니다. |
| VD_E_NOTSUPPORTED | 구성에 있는 하나 이상의 필드가 잘못되었거나 지원되지 않습니다. |
| VD_E_PROTOCOL | 가상 디바이스 세트가 생성되었습니다. |

## <a name="remarks"></a>Remarks

CreateEx 메서드는 BACKUP 또는 RESTORE 작업당 한 번만 호출해야 합니다. Close 메서드를 호출한 후 클라이언트는 인터페이스를 다시 사용하여 다른 가상 디바이스 세트를 만들 수 있습니다.

인스턴스 이름은 Transact-SQL이 발급된 인스턴스를 식별해야 합니다. NULL은 기본 인스턴스를 식별합니다. "machineName\" 접두사는 허용되지 않습니다.

CreateEx(및 Create) 호출은 클라이언트 프로세스의 프로세스 핸들에서 보안 DACL을 수정합니다. 따라서 프로세스 핸들의 다른 수정 내용은 CreateEx를 호출하여 직렬화해야 합니다. CreateEx는 CreateEx에 대한 다른 호출로 직렬화되지만 외부 처리로는 직렬화할 수 없습니다. SQL Server 서비스를 실행하는 계정에 액세스 권한이 부여됩니다.

CreateEx 메서드는 원본 IClientVirtualDeviceSet에 정의된 Create 메서드를 대체합니다. 원본 Create 메서드는 더 이상 사용되지 않으므로 향후 개발에 사용하면 안 됩니다. 원본 Create 메서드는 _VIRTUAL_SERVER_NAME_ 환경 변수를 사용하여 인스턴스 이름 지원 형식을 구현합니다. 환경에 해당 변수가 설정된 경우 Create 메서드는 _VIRTUAL_SERVER_NAME_의 값을 인스턴스 이름으로 제공하여 내부적으로 CreateEx를 호출합니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.