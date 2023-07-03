# Recover User

`POST /auth/recover`

Recovers a user, using a recovery credential. After successfully recovering the user, all of the user's previous credentials and personal access tokens will be invalidated.

{% hint style="info" %}
* Request headers required. See [Request Headers](../../../getting-started/request-headers.md) for more information.
* Temporary authentication token required. See [Registration Headers](../../../getting-started/request-headers.md#registration-headers) for more information.
{% endhint %}

## Required Permissions

{% hint style="info" %}
Since this endpoint is not authentication, the permissions apply to the application only.
{% endhint %}

| Name                  | Conditions                        |
| --------------------- | --------------------------------- |
| `Auth:Users:Create`   | Always Required                   |
| `Auth:Types:Employee` | When `kind` is `CustomerEmployee` |
| `Auth:Types:EndUser`  | When `kind` is `EndUser`          |

## Request body

| | | |
| - | - | - |
| `recovery` <mark style="color:red;">\*</mark> | `Object` | a signature of the user's new credentials, using the user's recovery credential, that proves the user initiated the recovery request |
| `recovery.kind` <mark style="color:red;">\*</mark> | `String` | will always be `RecoveryKey` |
| `recovery.credentialAssertion` <mark style="color:red;">\*</mark> | `Object` | |
| `recovery.credentialAssertion.credId` <mark style="color:red;">\*</mark> | `String` | base64url encoded id of the recovery credential |
| `recovery.credentialAssertion.clientData` <mark style="color:red;">\*</mark> | `String` | base64url encoded [Client Data](../../../advanced-topics/authentication/credentials/user-credentials.md#recovery-client-data-format) JSON string object that was signed with the user's private key |
| `recovery.credentialAssertion.signature` <mark style="color:red;">\*</mark> | `String` | base64url encoded signature generated by signing the clientData JSON string object |
| `newCredentials` <mark style="color:red;">\*</mark> | `Object` | the new credentials being assigned to the user |
| `newCredentials.firstFactorCredential` <mark style="color:red;">\*</mark> | `Object` | new first factor credential that the user is registering |
| `newCredentials.secondFactorCredential` | `Object` | `Optional` new second factor credential that the user is registering |
| `newCredentials.recoveryCredential` | `Object` | `Optional` new recovery credential that can be used to recover the user's account |

### Fido2 Credential

| | | |
| ------ | ----------------- | ----------- |
| `credentialKind` <mark style="color:red;">\*</mark> | `String` | will always be `Fido2` |
| `credentialInfo` <mark style="color:red;">\*</mark> | `Object` | |
| `credentialInfo.credId` <mark style="color:red;">\*</mark> | `String` | base64url encoded id of the credential |
| `credentialInfo.clientData` <mark style="color:red;">\*</mark> | `String` | base64url encoded client data object. The underlying object is the clientData object returned by the user's WebAuthn client |
| `credentialInfo.attestationData` <mark style="color:red;">\*</mark> | `String` | base64url encoded attestation data object. The underlying object is the attestationData object returned by the user's WebAuthn client |

Example:
```JSON
{
  "recovery":{
    "kind":"RecoveryKey",
    "credentialAssertion":{
      "credId":"d0MjPWGaRYS4H9fpubGCMCw7mhUCu3hP3NAkRtdGNK0",
      "clientData":"eyJ0eXBlIjoia2V5LmdldCIsImNoYWxsZW5nZSI6Ik1XTTBNbVk1WVRRME1EUmlOemRoTlRGaE56WTVPRFF3TldJNVpUUTRZMlJoT0RaaU5EazNaVFl6T1RFNU9HWXlNRGN4WmpCall6azRNbVE1WXpZMU1BIiwib3JpZ2luIjoiaHR0cHM6Ly9hcHAuZGZucy5uaW5qYSIsImNyb3NzT3JpZ2luIjpmYWxzZX0",
      "signature":"b6-3t95LkFnXhL6F8MDBHdUBsrVdm9wycq9SCsJhyiHph9uaVCJw9Vb-TlO1ILLKJvmoPELyx7XjpAC9Ww65UA",
    }
  },
  "newCredentials":{
    "firstFactorCredential":{
      "credentialKind":"Fido2",
      "credentialInfo":{
        "credId":"c1QEdgnPLJargwzy3cbYKny4Q18u0hr97unXsF3DiE8",
        "clientData":"eyJ0eXBlIjoid2ViYXV0aG4uY3JlYXRlIiwiY2hhbGxlbmdlIjoiTVdNME1tWTVZVFEwTURSaU56ZGhOVEZoTnpZNU9EUXdOV0k1WlRRNFkyUmhPRFppTkRrM1pUWXpPVEU1T0dZeU1EY3haakJqWXprNE1tUTVZelkxTUEiLCJvcmlnaW4iOiJodHRwczovL2FwcC5kZm5zLm5pbmphIiwiY3Jvc3NPcmlnaW4iOmZhbHNlfQ",
        "attestationData":"WT-zFZUBbJHfBkmhzTlPf49LTn7asLeTQKhm_riCvFgFAAAAAA"
      }
    },
    "recoveryCredential":{
      "credentialKind":"RecoveryKey",
      "credentialInfo":{
        "credId":"GMkW0zlmcoMxI1OX0Z96LL_Mz7dgeu6vOH5_TOeGyNk",
        "clientData":"eyJ0eXBlIjoia2V5LmNyZWF0ZSIsImNoYWxsZW5nZSI6Ik1XTTBNbVk1WVRRME1EUmlOemRoTlRGaE56WTVPRFF3TldJNVpUUTRZMlJoT0RaaU5EazNaVFl6T1RFNU9HWXlNRGN4WmpCall6azRNbVE1WXpZMU1BIiwib3JpZ2luIjoiaHR0cHM6Ly9hcHAuZGZucy5uaW5qYSIsImNyb3NzT3JpZ2luIjpmYWxzZX0",
        "attestationData":"Wsdz5810zjVJEyEtx9jYU0dizfhIkdu9AOGl2kYtcBusAPsfjdncE6zKW8ms_VkhJ6Hw4HDfcYj5FHcdM-C4CA"
      },
      "encryptedPrivateKey":"LsXVskHYqqrKKxBC9KvqStLEmxak5Y7NaboDDlRSIW7evUJpQTT1AYvx0EsFskmriaVb3AjTCGEv7gqUKokml1USL7+dVmrUVhV+cNWtS5AorvRuZr1FMGVKFkW1pKJhFNH2e2O661UhpyXsRXzcmksA7ZN/V37ZK7ITue0gs6I="
    }
  }
}
```

### Key Credential

| | | |
| ------ | ----------------- | ----------- |
| `credentialKind` <mark style="color:red;">\*</mark> | `String` | will always be `Key` |
| `credentialInfo` <mark style="color:red;">\*</mark> | `Object` | |
| `credentialInfo.credId` <mark style="color:red;">\*</mark> | `String` | base64url encoded id of the credential |
| `credentialInfo.clientData` <mark style="color:red;">\*</mark> | `String` | base64url encoded [Client Data](../../../advanced-topics/authentication/credentials/user-credentials.md#client-data-format) JSON string object that was signed with the user's private key |
| `credentialInfo.attestationData` <mark style="color:red;">\*</mark> | `String` | base64url encoded [Credential Assertion](../../../advanced-topics/authentication/credentials/user-credentials.md#credential-assertion) JSON string object with the user's signature and public key |

Example:
```JSON
{
  "recovery":{
    "kind":"RecoveryKey",
    "credentialAssertion":{
      "credId":"d0MjPWGaRYS4H9fpubGCMCw7mhUCu3hP3NAkRtdGNK0",
      "clientData":"eyJ0eXBlIjoia2V5LmdldCIsImNoYWxsZW5nZSI6Ik1XTTBNbVk1WVRRME1EUmlOemRoTlRGaE56WTVPRFF3TldJNVpUUTRZMlJoT0RaaU5EazNaVFl6T1RFNU9HWXlNRGN4WmpCall6azRNbVE1WXpZMU1BIiwib3JpZ2luIjoiaHR0cHM6Ly9hcHAuZGZucy5uaW5qYSIsImNyb3NzT3JpZ2luIjpmYWxzZX0",
      "signature":"b6-3t95LkFnXhL6F8MDBHdUBsrVdm9wycq9SCsJhyiHph9uaVCJw9Vb-TlO1ILLKJvmoPELyx7XjpAC9Ww65UA",
    }
  },
  "newCredentials":{
    "firstFactorCredential":{
      "credentialKind":"Key",
      "credentialInfo":{
        "credId":"6Ca6tAOFTx2odyJBnCoRO-gPvfpfy0EOoOcEaxfxIOk",
        "clientData":"eyJ0eXBlIjoia2V5LmNyZWF0ZSIsImNoYWxsZW5nZSI6Ik1XTTBNbVk1WVRRME1EUmlOemRoTlRGaE56WTVPRFF3TldJNVpUUTRZMlJoT0RaaU5EazNaVFl6T1RFNU9HWXlNRGN4WmpCall6azRNbVE1WXpZMU1BIiwib3JpZ2luIjoiaHR0cHM6Ly9hcHAuZGZucy5uaW5qYSIsImNyb3NzT3JpZ2luIjpmYWxzZX0",
        "attestationData":"WT-zFZUBbJHfBkmhzTlPf49LTn7asLeTQKhm_riCvFgFAAAAAA"
      }
    },
    "recoveryCredential":{
      "credentialKind":"RecoveryKey",
      "credentialInfo":{
        "credId":"GMkW0zlmcoMxI1OX0Z96LL_Mz7dgeu6vOH5_TOeGyNk",
        "clientData":"eyJ0eXBlIjoia2V5LmNyZWF0ZSIsImNoYWxsZW5nZSI6Ik1XTTBNbVk1WVRRME1EUmlOemRoTlRGaE56WTVPRFF3TldJNVpUUTRZMlJoT0RaaU5EazNaVFl6T1RFNU9HWXlNRGN4WmpCall6azRNbVE1WXpZMU1BIiwib3JpZ2luIjoiaHR0cHM6Ly9hcHAuZGZucy5uaW5qYSIsImNyb3NzT3JpZ2luIjpmYWxzZX0",
        "attestationData":"Wsdz5810zjVJEyEtx9jYU0dizfhIkdu9AOGl2kYtcBusAPsfjdncE6zKW8ms_VkhJ6Hw4HDfcYj5FHcdM-C4CA"
      },
      "encryptedPrivateKey":"LsXVskHYqqrKKxBC9KvqStLEmxak5Y7NaboDDlRSIW7evUJpQTT1AYvx0EsFskmriaVb3AjTCGEv7gqUKokml1USL7+dVmrUVhV+cNWtS5AorvRuZr1FMGVKFkW1pKJhFNH2e2O661UhpyXsRXzcmksA7ZN/V37ZK7ITue0gs6I="
    }
  }
}
```

### Recovery Credential

| | | |
| ------ | ----------------- | ----------- |
| `credentialKind` <mark style="color:red;">\*</mark> | `String` | will always be `RecoveryKey` |
| `credentialInfo` <mark style="color:red;">\*</mark> | `Object` | |
| `credentialInfo.credId` <mark style="color:red;">\*</mark> | `String` | base64url encoded id of the credential |
| `credentialInfo.clientData` <mark style="color:red;">\*</mark> | `String` | base64url encoded [Client Data](../../../advanced-topics/authentication/credentials/user-credentials.md#client-data-format) JSON string object that was signed with the user's private key |
| `credentialInfo.attestationData` <mark style="color:red;">\*</mark> | `String` | base64url encoded [Credential Assertion](../../../advanced-topics/authentication/credentials/user-credentials.md#credential-assertion) JSON string object with the user's signature and public key |
| `encryptedPrivateKey` | `String` | `Optional` encrypted private key. The user should hold the secret to decrypting this value, and that secret should never be transmitted to Dfns |

Example:
```JSON
{
  "recovery":{
    "kind":"RecoveryKey",
    "credentialAssertion":{
      "credId":"d0MjPWGaRYS4H9fpubGCMCw7mhUCu3hP3NAkRtdGNK0",
      "clientData":"eyJ0eXBlIjoia2V5LmdldCIsImNoYWxsZW5nZSI6Ik1XTTBNbVk1WVRRME1EUmlOemRoTlRGaE56WTVPRFF3TldJNVpUUTRZMlJoT0RaaU5EazNaVFl6T1RFNU9HWXlNRGN4WmpCall6azRNbVE1WXpZMU1BIiwib3JpZ2luIjoiaHR0cHM6Ly9hcHAuZGZucy5uaW5qYSIsImNyb3NzT3JpZ2luIjpmYWxzZX0",
      "signature":"b6-3t95LkFnXhL6F8MDBHdUBsrVdm9wycq9SCsJhyiHph9uaVCJw9Vb-TlO1ILLKJvmoPELyx7XjpAC9Ww65UA",
    }
  },
  "newCredentials":{
    "firstFactorCredential":{
      "credentialKind":"Key",
      "credentialInfo":{
        "credId":"6Ca6tAOFTx2odyJBnCoRO-gPvfpfy0EOoOcEaxfxIOk",
        "clientData":"eyJ0eXBlIjoia2V5LmNyZWF0ZSIsImNoYWxsZW5nZSI6Ik1XTTBNbVk1WVRRME1EUmlOemRoTlRGaE56WTVPRFF3TldJNVpUUTRZMlJoT0RaaU5EazNaVFl6T1RFNU9HWXlNRGN4WmpCall6azRNbVE1WXpZMU1BIiwib3JpZ2luIjoiaHR0cHM6Ly9hcHAuZGZucy5uaW5qYSIsImNyb3NzT3JpZ2luIjpmYWxzZX0",
        "attestationData":"WT-zFZUBbJHfBkmhzTlPf49LTn7asLeTQKhm_riCvFgFAAAAAA"
      }
    },
    "recoveryCredential":{
      "credentialKind":"RecoveryKey",
      "credentialInfo":{
        "credId":"GMkW0zlmcoMxI1OX0Z96LL_Mz7dgeu6vOH5_TOeGyNk",
        "clientData":"eyJ0eXBlIjoia2V5LmNyZWF0ZSIsImNoYWxsZW5nZSI6Ik1XTTBNbVk1WVRRME1EUmlOemRoTlRGaE56WTVPRFF3TldJNVpUUTRZMlJoT0RaaU5EazNaVFl6T1RFNU9HWXlNRGN4WmpCall6azRNbVE1WXpZMU1BIiwib3JpZ2luIjoiaHR0cHM6Ly9hcHAuZGZucy5uaW5qYSIsImNyb3NzT3JpZ2luIjpmYWxzZX0",
        "attestationData":"Wsdz5810zjVJEyEtx9jYU0dizfhIkdu9AOGl2kYtcBusAPsfjdncE6zKW8ms_VkhJ6Hw4HDfcYj5FHcdM-C4CA"
      },
      "encryptedPrivateKey":"LsXVskHYqqrKKxBC9KvqStLEmxak5Y7NaboDDlRSIW7evUJpQTT1AYvx0EsFskmriaVb3AjTCGEv7gqUKokml1USL7+dVmrUVhV+cNWtS5AorvRuZr1FMGVKFkW1pKJhFNH2e2O661UhpyXsRXzcmksA7ZN/V37ZK7ITue0gs6I="
    }
  }
}
```

## Responses

{% hint style="info" %}
* See [Common Errors](../../../getting-started/errors.md#common-errors) for common errors.
* See [User Recovery Errors](../../../getting-started/errors.md#user-recovery-errors) for user recovery specific errors.
{% endhint %}

{% tabs %}
{% tab title="200" %}
**Success** - an object describing the user

```JSON
{
  "credential": {
    "uuid": "cr-34514-nip9c-8bppvgqgj28dbodrc",
    "kind": "Fido2",
    "name": "Default Credential"
  },
  "user": {
    "id": "us-2ba0h-lvp2q-8v1860pcj1bh5irf",
    "username": "jdoe@example.co",
    "orgId": "or-34513-nip9c-8bppvgqgj28dbodrc"
  }
}
```
{% endtab %}
{% endtabs %}

## Examples