1. To create the pipeline first configure the dirctory structure:
    .github/workflows
2. Creat the pipeline "P1" in the workflow directory and configure the below configurations:
    - Add the name of the workflow.
    - Set the trigger
    - Give the write permisson.
    - Create Job and set the Git User and other necessary configurations (mentioned in P1.yaml).
3. For configuring pipeline P2: -
    - The pipeline P2 will run only if the pipelie P1 is successful, to achieve this use: 
    ```bash
        - on:
            workflow_run:
                workflows: ["P1"]
                types:
                    - completed
    ```
    - To check if the pipeline P1 is successful or not we will use: -
    ```bash
        if: ${{ github.event.workflow_run.conclusion == 'success' }}
    ```
    - To setup notification on Telegram :
        - Get telegram bot token and CHAT ID and set it as secrets in the repo.
        - Then use the action: -
          ```bash
            "appleboy/telegram-action@master" and pass the token and chat_id
          ```
        - At last write the message that would be sent to the telegram 
    (Follow Same steps are done for the Pipeline P3 when the pipeline P1 is unsuccessfull)