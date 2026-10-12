# Snapfit: Additional Product Direction Brainstorming

- **Date:** 2026-10-12
- **Status:** Exploration to consider; not an approved implementation scope.
- **Related specification:** [SRS & System Architecture](Software_Requirement_Specification_\(SRS\)_&_System_Architecture.md)
- **Purpose:** Preserve the user's problem statement and explore how it could shape Snapfit's product experience and technical requirements.

## 1. User-Stated Problems

The user identified six problems the app should solve. The following wording preserves their intent:

1. Users do not know what to wear.
2. Users do not want to discover after purchasing that an item is different from what they expected.
3. Users do not want to waste time waiting for delivery and then arranging a return.
4. Users want to see how they would look in a real situation before purchasing.
5. Users want to feel confident in what they wear.
6. Users want an AI assistant that understands what suits them, without having to explain their needs repeatedly.

These problems are the user-confirmed basis of this note. The solutions, positioning, technical approaches, and validation methods below are proposals to evaluate.

## 2. Proposed Product Direction

**Snapfit helps users feel confident about what to wear and what to buy.**

Possible product promise:

> Know what works for you. See yourself wearing it. Decide with confidence.

The proposed centre of the product is a proactive personal fashion assistant. The digital wardrobe supplies knowledge of owned clothes; try-on helps visualize choices; product information helps evaluate purchases. Shopping and resale support those decisions.

This direction prioritizes useful outcomes over adding features solely to appear different. It does not establish that Snapfit is a market first, that it is a specific percentage different from competitors, or that users will prefer it without validation.

## 3. Proposed Experience A: Help Me Get Dressed

The assistant offers a small number of actionable outfits from the user's own wardrobe, with brief explanations and easy swaps.

Example:

> Here are two options for today. You usually prefer relaxed outfits, and you liked this combination last time. I've included your more comfortable shoes.

The explanation must reflect information the user actually supplied or behavior the system recorded. It must not invent preferences or claim comfort based on a photo.

Potential context includes occasion, weather, preferred coverage, comfort preferences, and available clothes. Calendar access is optional and consent-based. Laundry status, garment availability, and event details cannot be assumed if unknown.

The user can choose an outfit, swap a piece, save it, mark it as worn, or correct the assistant. Useful feedback includes “too formal,” “too warm,” “not comfortable,” and “not my style.” The app should not require a full wardrobe upload before providing initial value.

## 4. Proposed Experience B: Help Me Decide Before Buying

The user provides a supported product link or image. The assistant evaluates the candidate against the user's wardrobe and known preferences, then separates what it knows from what it cannot verify.

Potential output:

- Combinations with specific owned clothes.
- Relevant style, coverage, material, and care considerations based on available product data.
- A supported appearance preview on the user.
- Size guidance only where measurements and product information justify it.
- Missing information and uncertainties that could affect the decision.
- An owned-item alternative when the user can achieve the desired result without buying.

Example:

> This works with your navy trousers and cream skirt. The sleeves match your coverage preference. The size chart is missing garment measurements, so I can't confidently recommend a size yet.

Purchase advice should prioritize user suitability. Affiliate relationships must be disclosed and must not override preferences or suppress a useful no-purchase option.

## 5. Seeing the Outfit in a Situation

The user's goal is to understand how they would look in the intended setting, such as an office, outdoor lunch, interview, or evening event.

Possible exploration: contextual previews with simulated lighting and backgrounds, alongside the original product image and a simpler try-on view. A contextual scene must be labeled as simulated; a photorealistic image is not proof of physical accuracy.

Evaluate separately:

| Question | Evidence needed |
| --- | --- |
| Does this style work for the occasion? | User context, dress-code information, and explainable styling judgment |
| Does the preview preserve the garment? | Evaluation of color, silhouette, pattern, length, layering, and identity fidelity |
| Will this size fit? | Relevant user and garment measurements, size-chart quality, and validated fit methods |
| Will it feel comfortable? | User experience, preferences, material information, and practical constraints; cannot be established from a generated image |
| Will it arrive in time? | Current stock, dispatch and shipping information; an estimated date is not a guarantee |

Single-garment VTON remains the SRS baseline. Full-outfit and contextual generation require separate feasibility, quality, privacy, latency, and cost evaluation before being promised.

## 6. Proposed X Factor: Learn From What Actually Worked

The differentiation hypothesis is an assistant that connects its recommendations to the user's real wearing experience.

> Remember what looked good and what the user actually enjoyed wearing, then improve the next outfit or purchase recommendation.

Possible learning loop:

1. Suggest an outfit or evaluate a purchase using known context.
2. Record the user's selection, swaps, and corrections.
3. Optionally ask whether they wore it and how it felt.
4. Update explicit preferences and inferred tendencies separately.
5. Use that evidence in later advice, with a short explanation and a way to correct it.

Saving an inspiration image does not mean the user wants to wear everything in it. Clicking a product does not prove purchase satisfaction. Not returning an item does not prove good fit. Treat these signals with different confidence levels.

The assistant should express uncertainty, ask a focused question when needed, and avoid repeatedly asking about information it already knows. “Knows the user” should mean useful, consent-based personalization, not autonomous spending or unchallengeable judgment.

## 7. Technical Implications to Explore

These are candidate additions for a future SRS revision, not implementation commitments.

| Capability | Candidate technical work |
| --- | --- |
| Persistent understanding | Versioned preference records with provenance, confidence, user overrides, and deletion controls |
| Grounded conversation | Retrieve authorized wardrobe/product facts before generating advice; validate referenced item IDs and availability |
| Proactive recommendations | Trigger policies, opt-in context integrations, notification frequency controls, and user timezone handling |
| Outcome learning | Outfit-wear records, optional comfort/confidence feedback, purchase satisfaction and return reasons; distinguish observations from inference |
| Purchase evaluation | Product/variant normalization, measurement units, size-chart provenance, freshness, and missing-data handling |
| Situation previews | Separate model capability evaluation, scene controls, garment fidelity checks, and simulation disclosure |
| Recommendation quality | Versioned ranking, contextual evaluation, truthful explanation checks, diversity, and feedback-driven improvement |
| User control | Inspect, correct, reset, export, or delete remembered preferences and learning history |

An initial assistant can use explicit rules, retrieval, and ranking with conversational explanations. Training a custom model is not automatically necessary. Any model/provider choice should follow evaluation against the actual tasks.

## 8. Trust & Product Boundaries

- Support the user's chosen style and comfort; do not rank their body or present one beauty standard as objective truth.
- Keep body photos private and require appropriate consent for external processing. Memory and derived preference data are included in the privacy lifecycle.
- Explain appearance, fit, comfort, and delivery uncertainty independently.
- Aim to reduce avoidable purchase surprises and returns; do not promise perfect fit or zero returns.
- Present relevant choices without guaranteeing the assistant always knows best. Users retain control over clothing and purchase decisions.
- Do not infer sensitive traits from photos or behavior to personalize fashion advice. Ask for relevant preferences directly when needed.

## 9. Validation Before Expanding Scope

| Hypothesis | How to test | Useful evidence |
| --- | --- | --- |
| Daily advice solves a recurring problem | Observe target users choosing from suggestions using a small real wardrobe | Outfits actually worn, decision time, repeat use, reasons for rejection |
| Memory reduces repeated explanation | Compare later sessions with early sessions | Fewer repeated corrections, accurate remembered preferences, user-perceived relevance |
| Previews improve purchase understanding | Compare product-only decisions with preview-assisted decisions, then collect post-delivery feedback | Expectation gaps, garment-detail errors, confidence calibration |
| Advice reduces avoidable returns | Follow consented purchases and documented return reasons | Return reasons and rates with an appropriate comparison; distinguish size, quality, delivery, and preference issues |
| The assistant supports confidence | Ask optional feedback after real wear | User-reported comfort/confidence and whether the suggestion was useful; no fabricated objective confidence score |

Set success thresholds, evaluation samples, and observation periods before testing. Positive reactions to attractive generated images alone do not validate fit, purchase satisfaction, or sustained usefulness.

## 10. Open Questions & Relationship to the SRS

- Which initial audience and recurring dressing situation should the assistant serve first?
- What minimum onboarding and wardrobe input produces useful advice?
- Which information should be explicitly provided versus learned, and which context integrations are acceptable?
- How should the assistant handle insufficient measurements, low-quality images, unsupported garments, or conflicting preferences?
- Which preview capabilities can meet acceptable fidelity and cost targets?
- Which signals can be collected without turning the experience into burdensome logging?
- Should the first release emphasize daily dressing or pre-purchase confidence? Both are goals; sequencing remains undecided.

The existing SRS remains the technical baseline. This note does not approve a marketplace pivot, new billing rules, contextual/full-outfit generation, model training, or broader data collection. If this direction is adopted, map it into explicit functional requirements, privacy rules, API/data contracts, and acceptance criteria before implementation.
