// Function to update summary cards dynamically
function updateSummaryCards(data) {
    // 1. Calculate Total Revenue
    const totalRevenue = data
        .filter(item => item.category === 'revenue')
        .reduce((sum, item) => sum + item.total, 0);

    // 2. Calculate Total Variable Cost
    const totalCost = data
        .filter(item => item.category === 'cost')
        .reduce((sum, item) => sum + item.total, 0);

    // 3. Calculate Gross Margin
    const grossMargin = totalRevenue > 0 ? ((totalRevenue - totalCost) / totalRevenue) * 100 : 0;

    // 4. Calculate Cost Ratio
    const costRatio = totalRevenue > 0 ? (totalCost / totalRevenue) * 100 : 0;

    // 5. Update the HTML elements
    document.querySelector('.card.revenue .card-value').textContent = `฿${(totalRevenue / 1000000).toFixed(1)}M`;
    document.querySelector('.card.cost .card-value').textContent = `฿${(totalCost / 1000000).toFixed(2)}M`;
    document.querySelector('.card.margin .card-value').textContent = `${grossMargin.toFixed(1)}%`;
    document.querySelector('.card.efficiency .card-value').textContent = `${costRatio.toFixed(1)}%`;
}

// Call this function when the page loads
window.addEventListener('load', () => {
    initializeDashboard(); // Your existing function to create charts and table
    updateSummaryCards(budgetData); // Call the new function to update cards
});# my-dashboard
