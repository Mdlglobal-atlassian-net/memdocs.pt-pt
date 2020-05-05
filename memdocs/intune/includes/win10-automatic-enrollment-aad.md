## <a name="enable-windows-10-automatic-enrollment"></a>Ativar a inscrição automática de dispositivos Windows 10

A inscrição automática permite que os utilizadores inscrevam os respetivos dispositivos com Windows 10 no Intune. Para se inscreverem, os utilizadores adicionam as respetivas contas profissionais aos dispositivos pessoais ou associam os dispositivos pertencentes à empresa ao Azure Active Directory. Em segundo plano, o dispositivo é registado e associa-se ao Azure Active Directory. Depois de registado, o dispositivo é gerido com o Intune.

**Pré-requisitos**

- Subscrição do Azure Active Directory Premium ([subscrição de avaliação](https://go.microsoft.com/fwlink/?LinkID=816845))
- Subscrição do Microsoft Intune

### <a name="configure-automatic-mdm-enrollment"></a>Configurar a inscrição MDM automática

1. Inicie sessão no [portal do Azure](https://portal.azure.com) e selecione **Azure Active Directory**.

   ![Captura de ecrã a mostrar o portal do Azure](../enrollment/media/windows-enroll/auto-enroll-azure-main.png)

2. Selecione **Mobilidade (MDM e MAM)**.

   ![Captura de ecrã a mostrar o portal do Azure](../enrollment/media/windows-enroll/auto-enroll-mdm.png)

3. Selecione **Microsoft Intune**.

   ![Captura de ecrã a mostrar o portal do Azure](../enrollment/media/windows-enroll/auto-enroll-intune.png)

4. Configure **Âmbito do Utilizador de MDM**. Especifique quais os dispositivos dos utilizadores que devem ser geridos pelo Microsoft Intune. Os dispositivos com Windows 10 podem ser automaticamente inscritos na gestão com o Microsoft Intune.

   - **Nenhum** – Inscrição automática de MDM desativada
   - **Alguns** – Selecione os **Grupos** que podem inscrever automaticamente os dispositivos Windows 10
   - **Todos** – Todos os utilizadores podem inscrever automaticamente os dispositivos Windows 10

      > [!IMPORTANT]
      > Para os dispositivos ByOD do Windows, o âmbito do utilizador MAM tem precedência se tanto o âmbito do utilizador MAM como o âmbito do utilizador do MDM (inscrição automática de MDM) estiverem ativados para todos os utilizadores (ou os mesmos grupos de utilizadores). O dispositivo não será inscrito em MDM e as políticas de Proteção de Informação do Windows (WIP) serão aplicadas se os tiver configurado.
      >
      > Se a sua intenção é permitir a inscrição automática de dispositivos BYOD do Windows para um MDM: configurar o âmbito do utilizador do MDM para **Todos** (ou **Alguns**, e especificar um grupo) e configurar o âmbito do utilizador MAM para **Nenhum** (ou **Alguns**, e especificar um grupo - garantindo que os utilizadores não são membros de um grupo direcionado tanto pelos âmbitos de utilizadores do MDM como do MAM).
      >
      >Para [dispositivos corporativos,](../enrollment/enrollment-restrictions-set.md#blocking-personal-windows-devices)o âmbito do utilizador do MDM tem precedência se os âmbitos de utilizador do MDM e da MAM estiverem ativados. O dispositivo será automaticamente inscrito no MDM configurado.

   > [!NOTE]
   > O âmbito do utilizador do MDM deve ser definido para um grupo De AD Azure que contenha objetos de utilizador.

   ![Captura de ecrã a mostrar o portal do Azure](../enrollment/media/windows-enroll/auto-enroll-scope.png)

5. Utilize os valores predefinidos para os seguintes URLs:
    - **URL dos Termos de utilização de MDM**
    - **URL de Deteção de MDM**
    - **URL de Conformidade de MDM**

6. Selecione **Guardar**.

Por predefinição, a autenticação de dois fatores não está ativada para o serviço. No entanto, recomenda-se a autenticação de dois fatores aquando do registo de um dispositivo. Para ativar a autenticação de dois fatores, configure um fornecedor de autenticação de dois fatores no AD e configure as contas de utilizador para a autenticação multifator. Veja [Introdução ao Servidor Multi-Factor Authentication do Microsoft Azure](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).
