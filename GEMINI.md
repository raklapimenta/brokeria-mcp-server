# BrokerIA — Real Estate MCP Server

You have access to the BrokerIA MCP server, which provides tools for searching real estate listings in Brazil.

## Available Tools

### brokeria_buscar_imoveis
Search properties for sale or rent across Brazilian real estate agencies. Accepts natural language descriptions like "2 bedroom apartment in Campinas under 300k" or structured filters (city, neighborhood, type, bedrooms, price range, area, parking).

### brokeria_detalhes_imovel
Get complete details about a specific property: photos, description, features, pricing, location, and agency info. Requires the property UUID from search results.

### brokeria_simular_financiamento
Calculate mortgage payments using Brazilian SAC or PRICE systems. Returns first/average/last installment, total cost, and minimum required income. Default: 360 months, SAC system.

### brokeria_qualificar_lead
Register a qualified lead in the BrokerIA CRM. Requires name, phone, and agency slug. Creates a real record — always confirm data with the user before calling.

### brokeria_agendar_visita
Schedule a property visit. Requires property ID, visitor name, phone, and date/time (ISO 8601). Creates a real appointment — always confirm with the user.

## Guidelines

- **Currency**: All values are in BRL (Brazilian Real). Format as "R$ X.XXX,XX".
- **Language**: Properties are in Portuguese. Respond in the user's language but keep property names/addresses in Portuguese.
- **Financing**: Brazilian mortgage rules apply — banks typically require 20% down payment. MCMV (Minha Casa Minha Vida) program has special rates.
- **Lead registration**: Always confirm user's name, phone, and interest before calling qualificar_lead or agendar_visita.
- **Pagination**: Search returns up to 50 results. Use offset parameter for pagination.
- **309+ properties** from 10+ real estate agencies available.
