RESOURCE_GROUP := streamlit-demo
ACR_NAME := streamlitdemowebapps
APP_SERVICE_PLANE := demoappserviceplan
IMAGE_NAME := sample/demo

help: ## print this message
	@echo "Example operations by makefile."
	@echo ""
	@echo "Usage: make SUB_COMMAND argument_name=argument_value"
	@echo ""
	@echo "Command list:"
	@echo ""
	@printf "\033[36m%-30s\033[0m %-50s %s\n" "[Sub command]" "[Description]" "[Example]"
	@grep -E '^[/a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | perl -pe 's%^([/a-zA-Z_-]+):.*?(##)%$$1 $$2%' | awk -F " *?## *?" '{printf "\033[36m%-30s\033[0m %-50s %s\n", $$1, $$2, $$3}'


create-resourcegroup: ## create resource group ## make create-resourcegroup
	az group create --location japaneast --name $(RESOURCE_GROUP)


create-acr: ## create azure container registry ## create-acr
	az acr create -n $(ACR_NAME) -g $(RESOURCE_GROUP) --sku Standard


push-image: ## build and push image to ACR ## make push-image
	az acr build -t sample/demo -r $(ACR_NAME) .


create-appserviceplan: ## create app service plan ## make create-appserviceplan
	az appservice plan create --resource-group $(RESOURCE_GROUP) --name $(APP_SERVICE_PLANE) \
	    --is-linux --number-of-workers 1 --sku P1V2

create-webapps: ## create web apps from custom image ## make create-appserviceplan
	az webapp create --name streamlitdemowebapps --plan $(APP_SERVICE_PLANE) --resource-group $(RESOURCE_GROUP) \
		--deployment-container-image-name $(ACR_NAME).azurecr.io/$(IMAGE_NAME)

clear: ## clear Azure resource # make clear
	az group delete --name $(RESOURCE_GROUP)
