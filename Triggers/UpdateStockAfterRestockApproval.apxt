trigger UpdateStockAfterRestockApproval
on Re_Plastic_Innovations_Restock_Request__c (after update) {

    List<Re_Plastic_Innovations_Restock_Request__c> approvedRestocks =
        new List<Re_Plastic_Innovations_Restock_Request__c>();

    for (
        Re_Plastic_Innovations_Restock_Request__c restock
        : Trigger.new
    ) {

        Re_Plastic_Innovations_Restock_Request__c oldRestock =
            Trigger.oldMap.get(restock.Id);

        if (
            restock.Status__c == 'Approved' &&
            oldRestock.Status__c != 'Approved'
        ) {

            approvedRestocks.add(restock);
        }
    }

    if (!approvedRestocks.isEmpty()) {

        InventoryManager.processRestockApproval(
            approvedRestocks
        );

        EmailNotificationHelper.sendRestockNotification(
            approvedRestocks
        );
    }
}